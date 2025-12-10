## 🧩 Multi-Node Kubernetes Cluster Using Kind

This guide explains how to create and use a **3-node Kubernetes cluster** (1 control-plane + 2 workers) using **Kind**, including port exposure, context switching, deploying apps, and exposing services.


**1. Create a Multi-Node Kind Configuration File (`kind-config.yml`)**
```yml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  extraPortMappings:
    - containerPort: 30080
      hostPort: 30080
      protocol: TCP
- role: worker
- role: worker
```

> Port Mapping:
>   - Exposes NodePort 30080 from Kind’s control-plane node to your host machine
>   - Allows accessing services via  http://localhost:30080


**2. Create the Kind Cluster with Config**
```sh
kind create cluster --name <cluster-name> --config kind-config.yaml

# Verify nodes
kubectl get nodes
```

**3. Switch kubectl Context to this Cluster**
```sh
# List available contexts
kubectl config get-contexts

# Set the active context
kubectl config set-context <cluster-name>

# Confirm active context
kubectl config current-context

# Switch to this cluster if running multiple clusters
kubectl config use-context <cluster-name>
```

**4. Delete Cluster (Complete Reset)**
```sh
kind delete cluster --name <cluster-name>
```


**5. Test Deployment on Multi-Node Cluster**
```sh
# Create namespace
kubectl create ns <namespace>

# Apply pod
kubectl apply -f nginx-pod.yml

# Apply service
kubectl apply -f nginx-service.yml

# Access service in browser
http://localhost:30080
```


**6. Useful Commands**
```sh
kubectl get ns

kubectl get pods -n <namespace> -o wide

kubectl get svc -n <namespace> -o wide

kubectl get endpoints -n <namespace>
```