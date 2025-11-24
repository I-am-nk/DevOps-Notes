# Kubernetes

"Kubernetes is an open-source orchestration system for managing containerized applications across a cluster of machines. While Docker runs containers, Kubernetes automates deployment, scaling, and management of those containers in production."

---

## 🐳 Why Not Just Use Docker?

| Feature               | Docker Alone                      | Kubernetes                           |
|-----------------------|-----------------------------------|--------------------------------------|
| Container creation    | ✅ Yes                            | ✅ Yes (via Docker/Container Runtime) |
| Automatic scaling     | ❌ Manual                         | ✅ Yes (horizontal pod autoscaling)   |
| Load balancing        | ❌ Needs manual setup              | ✅ Built-in                           |
| Self-healing          | ❌ No                             | ✅ Yes                                |
| Rolling updates       | ❌ Needs custom script             | ✅ Built-in                           |
| Multi-container app mgmt | ❌ Manual networking & linking | ✅ Managed via Pods and Services      |
| Multi-host support    | ❌ No                             | ✅ Yes (clustered deployment)         |

---

## 🧱 Basic Kubernetes Concepts

| Component      | Description                                                          |
|--------------- |--------------------------------------------------------------------- |
| Pod            | The smallest unit in K8s; contains one or more containers            |
| Node           | A machine (physical or virtual) where containers run                 |
| Cluster        | A group of nodes managed by Kubernetes                               |
| Deployment     | Defines how to run and manage a set of pods (e.g., replicas, updates)|
| Service        | Exposes a set of Pods as a network service (with IP and load balancing)|
| Ingress        | Routes external traffic to Services based on rules (like a reverse proxy)|
| ConfigMap/Secret| Manage app configuration and sensitive data                         |
| Namespace      | Virtual clusters inside a K8s cluster for organizing apps            |

---

## 🛠 Tools That Work with Kubernetes

| Tool        | Purpose                               |
|-------------|---------------------------------------|
| kubectl     | CLI to interact with Kubernetes       |
| Helm        | Package manager for K8s apps          |
| Minikube    | Run Kubernetes locally                |
| K3s / Kind  | Lightweight K8s distributions         |
| Prometheus  | Monitoring                            |
| ArgoCD      | GitOps (K8s + Git) deployments        |

---

## Architecture of Kubernetes

Kubernetes architecture is divided into two main parts:
- Control Plane (Master components)
- Data Plane (Worker node components)

*The data plane is responsible for actually executing your actions, while the control plane is the one that is controlling these actions.*

---

### 1. Components in the Control Plane (Master Component)

#### API Server:
- Acts as the heart and core of Kubernetes.
- Accepts all incoming requests from the external world, including user requests to create resources like pods.
- Decides on necessary actions and interacts with other control plane components.
- Exposes Kubernetes to the external world; every cluster request is received by the API server.

#### Scheduler:
- Responsible for scheduling pods or other resources onto suitable worker nodes.
- The API server may decide a resource should be scheduled, and the scheduler determines which node (e.g., Node 1 or Node 2) is best suited for the task.

#### etcd:
- A key-value store where all Kubernetes cluster information is stored as objects or key-value pairs.
- Essential for restoring the cluster; without etcd, there is no cluster-related information.

#### Controller Manager:
- Supports features like Auto scaling, which relies on components called controllers (e.g., replica set).
- Ensures specified number of pod replicas are always running.
- Manages various inbuilt Kubernetes controllers, keeping them up and running.

#### CCM (Cloud Controller Manager):
- Relevant for Kubernetes on cloud platforms (AWS/EKS, Azure/AKS, Google Cloud/GKE).
- Translates Kubernetes requests into cloud provider API commands.
- Supports cloud-platform-specific logic; not required for on-premise Kubernetes.

---

### 2. Components Found in the Data Plane (Worker Node)

#### Cubelet:
- Present on each worker node.
- Responsible for running your pod and ensuring pods are always in a **running state**.
- Alerts control plane if pods are not running for further action.

#### kube-proxy:
- Provides networking for pods and containers.
- Allocates IPs, enables load balancing, sets up network rules (IP tables).
- Distributes requests between pod replicas during autoscaling.
- Present on every worker node.

#### Container Runtime:
- Actually runs your container.
- Examples: Docker shim, containerd, CRI-O (Kubernetes supports multiple runtimes).
- Responsible for running containers inside pods.

*These three components on the worker node provide essential functionality to run your application.*

---

**Summary:**
- Cubelet handles deployment,
- kube-proxy handles networking,
- Container runtime provides the execution environment.

---

We run the pods in Kubernetes as we run containers in Docker,  
but running pods in Kubernetes requires a YAML file; we do not directly run it via the CLI.
