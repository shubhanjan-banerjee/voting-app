for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
 "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
 "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
 sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
docker login

curl -s https://fluxcd.io/install.sh | sudo bash

mkcert -key-file key.pem -cert-file cert.pem dev.cognizant.com \*.cognizant.com
mkcert -install

LINUX:
export GITHUB_TOKEN=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
export GITHUB_USER=shubhanjan-banerjee

WINDOWS:
set GITHUB_TOKEN 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
set GITHUB_USER shubhanjan-banerjee

sudo service docker start
sudo minikube start --force

echo $GITHUB_USER

flux check --pre

flux bootstrap github --owner=$GITHUB_USER --repository=voting-app-env --branch=main --read-write-key --personal --path=./clusters/my-cluster --token-auth=true

flux reconcile kustomization flux-system --with-source

flux create source git votingapp --url=https://github.com/shubhanjan-banerjee/voting-app-env --branch=main --interval=1m --export > ./clusters/my-cluster/votingapp-source.yaml

flux create kustomization votingapp --target-namespace=default --source=votingapp --path="./clusters/kustomize/" --prune=true --wait=true --interval=30m --retry-interval=2m --health-check-timeout=3m --export > ./clusters/my-cluster/votingapp-kustomization.yaml

flux reconcile kustomization votingapp --with-source

sudo minikube stop
sudo service docker stop
