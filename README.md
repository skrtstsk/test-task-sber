# Requirements:
docker - 
minikube -
kubectl -
helm - 
# Install minikube
Download minikube:
```
New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force
Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing
```
Add the minikube.exe binary to PATH:
```
$oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
if ($oldPath.Split(';') -inotcontains 'C:\minikube'){
  [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine)
}
```
Start a minikube:
```
minikube start -driver=docker
```
Verify minikube is running:
```
minikube get nodes
```
# Install helm 
Installing from script:
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
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
