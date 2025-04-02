### **What is a Namespace in Kubernetes?**
A **Namespace** in Kubernetes is a logical partition within a cluster that helps organize and manage resources efficiently. It allows multiple teams or projects to use the same cluster **without interference** by providing isolation.

---

## **Key Features of Namespaces**
- **Resource Isolation:** Different teams/projects can operate in their own environments.
- **Resource Quotas:** You can limit CPU, memory, and storage usage for each namespace.
- **Access Control:** Role-Based Access Control (**RBAC**) can restrict user permissions per namespace.
- **Scoped Objects:** Services, Pods, ConfigMaps, and other resources belong to specific namespaces.

---

## **Default Namespaces in Kubernetes**
Kubernetes comes with some built-in namespaces:
1. **`default`** – The default namespace for all resources when no namespace is specified.
2. **`kube-system`** – Contains Kubernetes system components (e.g., `kube-dns`, `kube-proxy`).
3. **`kube-public`** – Public resources, readable by everyone (rarely used).
4. **`kube-node-lease`** – Tracks node heartbeat leases (for node health checks).

---

## **Basic Namespace Commands**
### **1. List All Namespaces**
```sh
kubectl get namespaces
or 
kubectl get ns
kubectl get pod -n <custom namespace>
  - which is used list pod deploy under the custom namesapce
```

### **2. Create a New Namespace**
```sh
kubectl create namespace my-namespace
```

### **3. Deploy Resources in a Specific Namespace**
```sh
kubectl apply -f my-app.yaml --namespace=my-namespace
```
Or specify it inside your YAML:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: my-namespace
spec:
  containers:
    - name: nginx
      image: nginx
```

### **4. Switch to a Different Namespace (Set Default)**
```sh
kubectl config set-context --current --namespace=my-namespace
```

### **5. Delete a Namespace**
```sh
kubectl delete namespace my-namespace
```

---

## **When to Use Namespaces?**
- Large clusters with multiple teams/projects.
- Need for **resource separation** and quotas.
- Implementing **security policies** per namespace.

For small clusters, **one namespace (default) is enough**. 🚀

