# 🚀 Kubernetes kubectl Commands — Tabular Cheat Sheet

| Category | Command | Description |
|---------|---------|-------------|
| **1️⃣ Check Cluster & Nodes** | `kubectl cluster-info` | Show cluster info |
| | `kubectl get nodes` | List all nodes |
| | `kubectl describe node <node-name>` | Detailed node information |
| **2️⃣ Pod Operations** | `kubectl get pods` | List all pods |
| | `kubectl get pods -o wide` | List pods with Node/IP details |
| | `kubectl describe pod <pod-name>` | Describe a specific pod |
| | `kubectl logs <pod-name>` | Show pod logs |
| | `kubectl exec -it <pod-name> -- /bin/bash` | Access pod shell |
| | `kubectl delete pod <pod-name>` | Delete a pod |
| **3️⃣ Deployment Operations** | `kubectl create deployment <name> --image=<image>` | Create a deployment |
| | `kubectl get deployments` | List deployments |
| | `kubectl describe deployment <name>` | Detailed deployment description |
| | `kubectl scale deployment <name> --replicas=3` | Scale deployment |
| | `kubectl rollout restart deployment <name>` | Restart deployment |
| | `kubectl delete deployment <name>` | Delete deployment |
| **4️⃣ Service Operations** | `kubectl expose deployment <name> --type=NodePort --port=80` | Expose deployment as service |
| | `kubectl get svc` | List services |
| | `kubectl delete svc <service-name>` | Delete a service |
| **5️⃣ YAML Config Operations** | `kubectl apply -f <file.yaml>` | Create/Update resource from YAML |
| | `kubectl get all` | List all k8s resources |
| | `kubectl delete -f <file.yaml>` | Delete using YAML file |
| **6️⃣ Namespace Operations (Optional)** | `kubectl get namespaces` | List namespaces |
| | `kubectl create namespace <name>` | Create namespace |
| | `kubectl delete namespace <name>` | Delete namespace |
| **🔹 Minikube Commands** | `minikube start` | Start Minikube cluster |
| | `minikube stop` | Stop Minikube cluster |
| | `minikube status` | Show Minikube status |
| | `minikube service <service-name>` | Get service URL |
