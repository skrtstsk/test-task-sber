## Requirements:
Docker - [Docker installation](https://docs.docker.com/engine/install/) <br />
Minikube - [Minikube installation](https://minikube.sigs.k8s.io/docs/start/) <br />
Kubectl - [Kubectl installation](https://kubernetes.io/ru/docs/tasks/tools/install-kubectl/) <br />
Helm - [Telm installation](https://helm.sh/docs/intro/install/) <br />
## Start a minikube
1. Start a minikube:
```
minikube start --driver=docker
```
2. Verify minikube nod is running:
```
kubectl get nodes
```
## Install jenkins
1. Create a namespace:
```
kubectl create namespace jenkins
```
3. Add repo:
```
helm repo add bitnami https://charts.bitnami.com/bitnami
```
3. Install repo:
```
helm install jenkins bitnami/jenkins -n default
```
4. Get the Jenkins URL:
```
minikube service jenkins -n jenkins
```
5. Login with: <br />
   Username: **user** <br />
   Password:  <br />
```
kubectl get secret --namespace jenkins my-release-jenkins -o jsonpath="{.data.jenkins-password}"
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("<insert ouput from previous command>"))
```
## Set up jenkins
1. Install plugins: Kubernetes, Credentials
2. Dashboard -> Create Item -> Pipeline
3. Connect to git repo
   
![image](https://github.com/skrtstsk/test-task-sber/assets/91666235/f50e860e-2cbf-49be-ae32-6818d8610cf3)

4. Vefify deployment is READY
```
kubectl get deployments --all-namespaces
```
![image](https://github.com/skrtstsk/test-task-sber/assets/91666235/05838231-f113-4bdd-8032-a233922c2f5b)


   
