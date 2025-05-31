📌Presentation

🎯 Minikube Setup

For Minikube installation, we provide the installation with the necessary commands for Linux from the official website. https://minikube.sigs.k8s.io/docs/start
Here I installed it on a machine running Ubuntu on WSL.

"curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64"
"sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64"

After the Minikube installation was completed, we used Docker as the container runtime tool.

"sudo apt install docker.io"

Then we started the cluster.

"minikube start"

🎯 Application Deployment

We used a java application for deployment. https://github.com/benc-uk/java-demoapp

To deploy the application, we pulled the image pushed to the dockerhub address and defined it for deployment.

![alt text](image.png)

🎯 Ingress Configuration

We activated the ingress configuration in minikube to provide access via a domain address.

"minikube addons enable ingress"

![alt text](image-1.png)

We created a self-signed SSL certificate for HTTPS. We used openssl for this.

"openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=java-demoapp.example.com/O=java-demoapp"

We created a Kubernetes secret to provide the generated key and crt from outside.

kubectl create secret tls java-demoapp-tls --cert=tls.crt --key=tls.key

After deploying the manifest files, we used a tunnel to access the domain.

"minikube tunnel"

However, this is not enough. Since this address is not registered on any DNS server, we will access it via the local system. For this, we add the address to our hosts file.

"127.0.0.1 java-demoapp.example.com"

After the hosts file is saved, we can now access the address via the browser.

![alt text](image-2.png)

🎯 Testing and Validation

Our web application appears to be running, but there may be a problem with the backend services. If the pod is running but the API is not working, the pod will give an error and remain in the running state. To prevent this situation, we will use readiness and liveness probes in Kubernetes.

![alt text](image-3.png)

We receive a response about the status of the services at the "/actuator/health" endpoint. We used this for the liveness probe.

























