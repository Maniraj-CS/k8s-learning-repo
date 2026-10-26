# Kubernetes (K8s) Architecture 

Kubernetes works in a **cluster**, which is made of two main parts:

1. **Control Plane** → Brain of Kubernetes  
2. **Data Plane (Worker Nodes)** → Do the actual work

---

## 1. Control Plane (Brain of the Cluster)

The Control Plane decides:
- What should run
- Where it should run
- How to keep everything healthy

### 🔹 API Server
- Entry point of Kubernetes
- All commands go through the API Server  
  (`kubectl`, UI, CI/CD, etc.)
- It validates requests and talks to other components

👉 Think of it as the **front door** of Kubernetes.

---

### 🔹 etcd
- Key–value database
- Stores **entire cluster state**
  - Pods
  - Nodes
  - Configs
  - Secrets

👉 Think of it as the **memory or database** of Kubernetes.  
If etcd is lost → cluster state is lost.

---

### 🔹 Scheduler
- Decides **which Pod runs on which Node**
- Checks:
  - CPU
  - Memory
  - Resource availability

👉 Think of it as a **placement manager**.

---

### 🔹 Controller Manager
- Watches the cluster continuously
- Ensures **desired state = actual state**

Examples:
- If a Pod dies → create a new one
- If replicas are less → add more Pods

👉 Think of it as an **auto-fix system**.

---

### 🔹 Cloud Controller Manager (CCM)
- Connects Kubernetes with **cloud providers**
  (AWS, GCP, Azure, etc.)
- Manages:
  - Load Balancers
  - Cloud storage
  - Node lifecycle

👉 Think of it as a **cloud translator**.

---

## 2. Data Plane (Worker Nodes)

Worker Nodes are where applications actually run.

---

### 🔹 Kubelet
- Agent running on every worker node
- Talks to the API Server
- Makes sure Pods are running correctly

👉 Think of it as a **node supervisor**.

---

### 🔹 Kube-Proxy
- Handles networking
- Manages:
  - Service discovery
  - Load balancing inside the cluster

👉 Think of it as **traffic police**.

---

### 🔹 Container Runtime (Container Engine)
- Runs containers inside Pods
- Examples:
  - Docker
  - containerd
  - CRI-O

👉 Think of it as the **engine that runs containers**.

---

## How Everything Works Together (Flow)

1. User runs `kubectl apply`
2. Request goes to **API Server**
3. Data is stored in **etcd**
4. **Scheduler** chooses a Node
5. **Kubelet** creates the Pod
6. **Container Runtime** runs the container
7. **Controller Manager** keeps checking health
8. **Kube-Proxy** manages network traffic

---

## Easy One-Line Understanding

- **Control Plane** → Decides & manages  
- **Data Plane** → Executes & runs apps  

👉 Kubernetes = **Automatic manager for containers**
