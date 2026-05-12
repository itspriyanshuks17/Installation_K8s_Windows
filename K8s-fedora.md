# Install Kubernetes (kubectl) on Fedora

## Step 1 — Add Kubernetes Repo

Create repo file:

```bash id="e7wq1m"
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.30/rpm/repodata/repomd.xml.key
EOF
```

---

## Step 2 — Install kubectl

```bash id="l4vm8r"
sudo dnf install -y kubectl
```

Check:

```bash id="z0jmxv"
kubectl version --client
```

---

# Install Minikube on Fedora

## Step 1 — Install Minikube

```bash id="n2rc6x"
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

```bash id="x5pt9k"
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

Check:

```bash id="r7ha2d"
minikube version
```

---

# Start Kubernetes Cluster

Since Docker is installed:

```bash id="u3bz9n"
minikube start --driver=docker
```

This may take several minutes first time.

---

# Verify Cluster

```bash id="q8we1p"
kubectl get nodes
```

Expected:

```text
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   ...
```

---

# Enable Kubernetes Dashboard

```bash id="t9nk3c"
minikube dashboard
```

Opens browser dashboard automatically.

---

# Test Deployment

Create nginx deployment:

```bash id="y6cp2f"
kubectl create deployment nginx --image=nginx
```

Expose service:

```bash id="p4sl8j"
kubectl expose deployment nginx --type=NodePort --port=80
```

Check:

```bash id="m1gt5v"
kubectl get svc
```

Open app:

```bash id="v0qe7s"
minikube service nginx
```

---

# Useful Commands

## Cluster status

```bash id="c2rw9m"
minikube status
```

## Stop cluster

```bash id="f8du3k"
minikube stop
```

## Delete cluster

```bash id="j5lp7x"
minikube delete
```

---

# If Docker Driver Fails

Install virtualization:

```bash id="h6na4v"
sudo dnf install @virtualization -y
```

Enable libvirt:

```bash id="s3qy8w"
sudo systemctl enable --now libvirtd
```

Then:

```bash id="a1mz6n"
minikube start --driver=kvm2
```

---
