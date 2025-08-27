**basic app deployment on Amazon EKS**.
**simple Nginx app deployment on EKS** with clear steps.

---

---

## 📌 Prerequisites:

✅ AWS CLI configured (`aws configure`)
✅ `eksctl` installed
✅ `kubectl` installed
✅ EKS Cluster created

---

## 📦 1️⃣ Create EKS Cluster (if not created)

```bash
eksctl create cluster --name demo-cluster --region us-east-1 --nodes 2 --node-type t3.small
```

---

## 📄 2️⃣ Create Deployment Manifest `deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

---

## 📄 3️⃣ Create Service Manifest `service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

---

## 📥 4️⃣ Apply Manifests to EKS

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---

## 📊 5️⃣ Check Resources

```bash
kubectl get all
```

You'll see `pods`, `deployments`, and a `LoadBalancer`-type service.

---

## 🌐 6️⃣ Access Your App

Find your external ELB URL:

```bash
kubectl get svc nginx-service
```

Open the `EXTERNAL-IP` in your browser.

---

## 📦 Cleanup

```bash
kubectl delete -f service.yaml
kubectl delete -f deployment.yaml
```

Or to delete the cluster:

```bash
eksctl delete cluster --name demo-cluster
```

---

## 📌 Repo Structure (Optional Suggestion)

```
eks-basic-app/
├── deployment.yaml
├── service.yaml
├── README.md
```
---

