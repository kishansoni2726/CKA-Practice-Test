# 🚀 Q2: Add Sidecar Container to Existing Deployment

---

## 📘 Question

Update the existing deployment `wordpress`, adding a sidecar container named `sidecar` using the image `busybox:stable`.

### 📋 Requirements

- Sidecar should run:

```bash
/bin/bash -c "tail -f /var/log/wordpress.log"
Use a shared volume mounted at /var/log
Ensure log file wordpress.log is accessible to both containers
✅ Answer
🔹 Solution 1: Basic Sidecar Concept (Pod YAML)

This demonstrates how a sidecar container works using a standalone Pod.

apiVersion: v1
kind: Pod
metadata:
  labels:
    run: wordpress
  name: wordpress
spec:
  volumes:
  - name: log
    emptyDir: {}

  containers:
  - name: sidecar
    image: busybox:stable
    command: ["/bin/sh", "-c", "tail -f /var/log/wordpress.log"]
    volumeMounts:
    - name: log
      mountPath: /var/log

  - name: wordpress
    image: wordpress
    volumeMounts:
    - name: log
      mountPath: /var/log
🔹 Solution 2: Update Existing Deployment (Recommended)
⚙️ Environment Setup
1️⃣ Create Deployment
kubectl create deployment wordpress --image=wordpress
2️⃣ Verify Pod
kubectl get pods
🚀 Solution Steps
3️⃣ Edit Deployment
kubectl edit deployment wordpress
4️⃣ Final Deployment YAML (Relevant Changes Only)
spec:
  template:
    spec:
      containers:

      # ✅ Sidecar Container
      - name: sidecar
        image: busybox:stable
        command: ["/bin/sh", "-c", "tail -f /var/log/wordpress.log"]
        volumeMounts:
        - name: log
          mountPath: /var/log

      # ✅ Main Container
      - name: wordpress
        image: wordpress
        volumeMounts:
        - name: log
          mountPath: /var/log

      # ✅ Shared Volume
      volumes:
      - name: log
        emptyDir: {}
