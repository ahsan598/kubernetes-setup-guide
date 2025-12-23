# 🚀 Kubernetes Local Setup with KIND (Kubernetes in Docker)

**KIND = Kubernetes IN Docker**

Run Kubernetes inside Docker containers → Ideal for local DevOps practice, CI, and learning.


### 🔧 Installtion Steps

**1. Install Kubectl**
```sh
# Download latest kubectl binary
curl -LO "https://dl.k8s.io/release/$(curl -sL https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

chmod +x kubectl
sudo mv kubectl /usr/local/bin/

kubectl version --client      # verify
```

**2. Install Kind**
```sh
curl -Lo kind https://kind.sigs.k8s.io/dl/v0.30.0/kind-linux-amd64

chmod +x kind
sudo mv kind /usr/local/bin/kind

kind version                  # verify
```

**3. Create a Single-Node Kubernetes Cluster**
```sh
kind create cluster --name dev-cluster

# Verify
kubectl cluster-info
kubectl get nodes
```

> KIND clusters follow the naming: kind-cluster-name
> 
> Ex: kind-dev-cluster


**4. Switch kubectl Context**
```sh
kubectl config get-contexts        # list all
kubectl config use-context kind-dev-cluster   # switch active cluster
kubectl config current-context     # verify
```

> **NOTE:**
> `use-context` = switch the context
> `set-context` = modify context properties (does NOT switch)


**5. Delete Cluster (Full Reset)**
```sh
kind delete cluster --name dev-cluster
```


### 🧪 Kubernetes Basic Operations

**1. Create Deployment**
```sh
kubectl create deployment nginx --image=nginx -n default
kubectl get pods
```

**2. Expose Deployment (NodePort)**
```sh
kubectl expose deployment nginx \
  --type=NodePort \
  --name=nginx-svc \
  --port=80
```
Check service
```sh
kubectl get svc nginx-svc
```

**3. Port-Forwarding (local access)**
```sh
kubectl port-forward svc/nginx-svc 8080:80

# Access in browser:
http://localhost:8080
```

**4. Delete Deployment**
```sh
kubectl delete deployment nginx
```


### KIND Image Management Guide
```sh
# List kind clusters and nodes
kind get clusters
kind get nodes --name <cluster-name>

# View images inside KIND node (containerd images)
docker exec -it <node-name> crictl images

# Load local Docker image into KIND cluster
kind load docker-image <image-name>:<tag> --name <cluster-name>

# (Optional but Recommended) Verify image inside KIND
docker exec -it <node-name> crictl images | grep <image-name>:<tag>

# Login into KIND node (shell)
docker exec -it <node-name> bash

# List or Remove images (inside KIND)
crictl images
crictl rmi <image-name>:<tag> / crictl rmi <IMAGE_ID>

# Remove unused images inside KIND
crictl rmi --prune
```