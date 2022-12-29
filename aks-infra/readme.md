start AKS cluster

# pre-requsite 
virtual network rule to allow all traffic to be included
swap be turned off on every node swapoff -a

# setting up your cluster
1. download shell scripts k8scp.sh and k8sWorker.sh (note this shell uses Project Calico for networking this might not work best for Azure VM)
login to control plane vm
$ wget https://training.linuxfoundation.org/cm/LFD259/LFD259_V2022-11-23_SOLUTIONS.tar.xz --user=LFtraining --password=Penguin2014
$ tar -xvf LFD259_V2022-11-23_SOLUTIONS.tar.xz

2. deploy a new cluster Control Plane
login to worker vm
$ find $HOME -name k8scp.sh
$ more LFD259/SOLUTIONS/s_02/k8scp.sh
$ cp LFD259/SOLUTIONS/s_02/k8scp.sh .

NOTE: update k8scp.sh find below code and update to canal.yaml for Azure VM deployment
**kubectl apply -f https://projectcalico.docs.tigera.io/manifests/canal.yaml **

$ bash k8scp.sh | tee $HOME/cp.out
The kubeadm join statement can be found near the end of the kubeadm init output on the cp node.
$ grep -A2 join cp.out
this will be used to join with worker node

3. deploy a new worker node
login to worker vm
$ find $HOME -name k8sWorker.sh
$ cp LFD259/SOLUTIONS/s_02/k8sWorker.sh .
$ more k8sWorker.sh
$ bash k8sWorker.sh | tee worker.out

$ @worker:˜$ sudo kubeadm join --token 118c3e.83b49999dc5dc034 10.128.0.3:6443 --discovery-token-ca-cert-hash
sha256:40aa946e3f53e38271bae24723866f56c86d77efb49aedeb8a70cc189bfe2e1d

4. configure cp and worker : please refer to the pdf doc

# push image to github package
AzureAD+JayKim@LAB3-1228793957 MINGW64 ~/local/github/madforchili/jaykim-profile (main)
$ docker build -t jaykimprofile .

AzureAD+JayKim@LAB3-1228793957 MINGW64 ~/local/github/madforchili/jaykim-profile (main)
$ export CR_PAT=[github personal access token]

AzureAD+JayKim@LAB3-1228793957 MINGW64 ~/local/github/madforchili/jaykim-profile (main)
$ echo $CR_PAT | docker login ghcr.io -u madforchili --password-stdin
Login Succeeded

AzureAD+JayKim@LAB3-1228793957 MINGW64 ~/local/github/madforchili/jaykim-profile (main)
$ docker push ghcr.io/madforchili/jaykimprofile:latest
The push refers to repository [ghcr.io/madforchili/jaykimprofile]
a83da8676069: Pushed
0618d1e529fa: Pushed
6e96dd581d79: Pushed
acf5e0b2cf08: Pushed
d51445d70778: Pushed
b96b16a53835: Pushed
994393dc58e7: Pushed
latest: digest: sha256:d675f7669986cf7adcd0b858826db75981480f0729d0221a43ce3ef0207a9fb2 size: 1778




