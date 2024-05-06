# Requirements:
docker - https://docs.docker.com/engine/install/
minikube - https://minikube.sigs.k8s.io/docs/start/
kubectl - https://kubernetes.io/ru/docs/tasks/tools/install-kubectl/
helm - https://helm.sh/docs/intro/install/
# Start minikube
```
Start a minikube:
```
minikube start -driver=docker
```
Verify minikube is running:
```
minikube get nodes
```
# Install jenkins
Add repo:
```
helm repo add bitnami https://charts.bitnami.com/bitnami
```
Install repo:
```
helm install jenkins bitnami/jenkins -n default
```
Get the Jenkins URL:
```
minikube service jenkins -n jenkins
```
Login with:

Username: **user**

Password: 
```
kubectl get secret --namespace jenkins my-release-jenkins -o jsonpath="{.data.jenkins-password}"
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("<insert ouput from previous command>"))
```
