# Installing-Kubeadm

**Prerequisites:**

Ubuntu machine (Ubuntu 18.04 or later is recommended)

Root privileges or a user with sudo access
At least 2 virtual or physical machines (1 master node and 1 or more worker nodes)
Install Docker:
If you haven't already, install Docker on all the nodes. Kubernetes requires a container runtime, and Docker is a popular choice.

**1**
sudo apt update
sudo apt install docker.io

**
**Install kubeadm, kubelet, and kubectl:
Install the Kubernetes components kubeadm, kubelet, and kubectl on all the nodes.****


sudo apt update
sudo apt install -y kubelet kubeadm kubectl
**2**
**Initialize the Master Node:
Choose one node to be the master node and initialize it using kubeadm.
******

sudo kubeadm init

**3**
**Follow the instructions provided in the output to configure kubectl for your user.
**
Set Up kubectl for Your User:****
After initializing the master node, configure kubectl for your user:


mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

**4**
Install a Network Plugin:
To enable communication between pods across nodes, you need to install a network plugin. Popular choices include Calico, Flannel, and Weave. Here's an example of installing Calico:

kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

**5**
Join Worker Nodes:
If you have additional worker nodes, you need to join them to the cluster using the token generated during the master node initialization. On the master node, you can find the join command in the output of the kubeadm init command. It looks something like this:


kubeadm token create --print-join-command

Run this command on each worker node.
**6**
Verify Cluster Status:
After joining the worker nodes, you can verify the status of your cluster using:


kubectl get nodes
You should see the master node and worker nodes listed with their status as "Ready."

Congratulations! You've successfully set up a basic Kubernetes cluster using kubeadm. Remember that this is just a basic setup, and in a production environment, you'd need to consider additional configuration, security, and high-availability considerations.





to install kubectl , kubeadm, kubelet

sudo apt update
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt update
sudo apt install -y kubelet kubeadm kubectl
