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
### **Check Nodes  ** 
=============

kubectl get nodes



Deploy Sample Application
==========================

kubectl run nginx-demo --image=nginx --port=80 

kubectl expose pod nginx-demo --port=80 --target-port=80 --type=NodePort --namespace=prod


Get Node Port details 
=====================
kubectl get services
  ubuntu@ip-192-168-1-203:~$ kubectl get service
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   129m
ubuntu@ip-192-168-1-203:~$

Get All pod details
=====================
kubectl get pod -n --all-namespaces
 - to list all pods under each namespaces
ex: 
ubuntu@ip-192-168-1-203:~$ kubectl get po --all-namespaces
NAMESPACE     NAME                                       READY   STATUS    RESTARTS       AGE
kube-system   coredns-7c65d6cfc9-4p8hz                   1/1     Running   0              128m
kube-system   coredns-7c65d6cfc9-m7gd2                   1/1     Running   0              128m
kube-system   etcd-ip-192-168-1-203                      1/1     Running   0              128m
kube-system   kube-apiserver-ip-192-168-1-203            1/1     Running   0              128m
kube-system   kube-controller-manager-ip-192-168-1-203   1/1     Running   0              128m
kube-system   kube-proxy-948m4                           1/1     Running   0              128m
kube-system   kube-proxy-9mp5n                           1/1     Running   0              118m
kube-system   kube-proxy-r9clp                           1/1     Running   0              118m
kube-system   kube-scheduler-ip-192-168-1-203            1/1     Running   0              128m
kube-system   weave-net-729tk                            2/2     Running   1 (122m ago)   122m
kube-system   weave-net-9dcwr                            2/2     Running   1 (117m ago)   118m
kube-system   weave-net-vqrgq                            2/2     Running   1 (117m ago)   118m
prob          nginx-demo                                 1/1     Running   0              109m


---

## **When to Use Namespaces?**
- Large clusters with multiple teams/projects.
- Need for **resource separation** and quotas.
- Implementing **security policies** per namespace.

For small clusters, **one namespace (default) is enough**. 🚀

