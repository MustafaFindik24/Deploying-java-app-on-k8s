📌Presentation

🎯Minikube Setup

For Minikube installation, we provide the installation with the necessary commands for Linux from the official website. https://minikube.sigs.k8s.io/docs/start
Here I installed it on a machine running Ubuntu on WSL.

curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

After the Minikube installation was completed, we used Docker as the container runtime tool.

sudo apt install docker.io

Then we started the cluster.

minikube start

🎯Application Deployment

https://github.com/benc-uk/java-demoapp/