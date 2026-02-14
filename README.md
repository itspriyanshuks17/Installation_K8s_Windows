# Installing Kubernetes (kubectl) and Minikube on Windows, Ubuntu, and macOS

This guide provides step-by-step instructions to install `kubectl` and `minikube` on **Windows**, **Ubuntu (Linux)**, and **macOS**.

---

## 🪟 Windows (Using Chocolatey)

### Prerequisites

* Windows 7 or later
* PowerShell or Command Prompt (Run as Administrator)
* Chocolatey installed
  👉 [https://chocolatey.org/install](https://chocolatey.org/install)

---

### Install `kubectl`

```sh
choco install kubernetes-cli
```

Verify:

```sh
kubectl version --client
```

Update:

```sh
choco upgrade kubernetes-cli
```

---

### Install Minikube

```sh
choco install minikube
```

Verify:

```sh
minikube version
```

Start cluster:

```sh
minikube start
```

Update:

```sh
choco upgrade minikube
```

---

## 🐧 Ubuntu (Linux)

### Prerequisites

* Ubuntu 20.04+
* sudo privileges
* `curl` installed
* A driver: Docker / VirtualBox / KVM

---

### Install `kubectl`

```sh
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update
sudo apt install -y kubectl
```

Verify:

```sh
kubectl version --client
```

---

### Install Minikube

```sh
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

Verify:

```sh
minikube version
```

Start cluster:

```sh
minikube start
```

Using Docker driver (recommended):

```sh
minikube start --driver=docker
```

---

## 🍎 macOS

### Prerequisites

* macOS 11+
* Homebrew installed
  👉 [https://brew.sh](https://brew.sh)
* Docker Desktop or another VM driver

---

### Install `kubectl`

```sh
brew install kubectl
```

Verify:

```sh
kubectl version --client
```

---

### Install Minikube

```sh
brew install minikube
```

Verify:

```sh
minikube version
```

Start cluster:

```sh
minikube start
```

With Docker driver:

```sh
minikube start --driver=docker
```

---

## 🔧 Verify Cluster (All OS)

```sh
kubectl get nodes
```

---

## 🔄 Updating

**Windows**

```sh
choco upgrade kubernetes-cli
choco upgrade minikube
```

**Ubuntu**

```sh
sudo apt update && sudo apt upgrade kubectl
```

**macOS**

```sh
brew upgrade kubectl
brew upgrade minikube
```

---

## 🧹 Uninstall

**Windows**

```sh
choco uninstall kubernetes-cli
choco uninstall minikube
```

**Ubuntu**

```sh
sudo apt remove kubectl
sudo rm /usr/local/bin/minikube
```

**macOS**

```sh
brew uninstall kubectl
brew uninstall minikube
```

---

## 🛠 Troubleshooting

* If Minikube won’t start:

  ```sh
  minikube delete
  minikube start --driver=docker
  ```
* Check cluster:

  ```sh
  kubectl cluster-info
  ```
* Check context:

  ```sh
  kubectl config current-context
  ```
