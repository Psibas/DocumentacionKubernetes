# 🧑🏽‍💻 Scripts de Instalación y Configuración de Kubernetes

Este documento contiene todos los comandos Bash utilizados en la instalación de Kubernetes en Ubuntu Server 24.0x.

---

## 🖥️ Instalación de kubeadm y Kubernetes
```bash
sudo apt update
sudo apt install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt update
sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

sudo kubeadm init --pod-network-cidr=192.168.0.0/16
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

kubectl taint nodes --all node-role.kubernetes.io/master-

kubectl get nodes
kubectl get pods --all-namespaces
