# Descomplicando_Kubernetes
Curso Descomplicando Kubernetes - LINUXTIPS

Pré-requisitos
- Docker instalado
- Kind instalado
- Kubectl instalado

## Instalação do Kind

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64
chmod +x ./kind
mv ./kind /usr/local/bin/kind
```
--------------------------------------------------------------------
## Instalação do Kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
mv kubectl /usr/local/bin/
```
---------------------------------------------------------------------
## Cria o Cluster Kubernetes com Kind
### Arquivo usado:
- kind-cluster.yaml

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```
---------------------------------------------------------------------
## Cria o cluster

```bash
kind create cluster --config kind-cluster.yaml

## Validação
kubectl get nodes
kubectl get pods -A
```
---------------------------------------------------------------------
## Pod de exemplo
### Arquivo usado:
- pod.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: darkside
  name: darkside
spec:
  containers:
  - image: nginx
    name: darkside
    ports:
    - containerPort: 80
```
---------------------------------------------------------------------
## Cria o Pod

```bash
kubectl apply -f pod.yaml

## Verificar o pod
kubectl get pods
kubectl describe pod darkside
```
