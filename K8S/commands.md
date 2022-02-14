- kubectl describe node nodename | grep Taints

kubectl taint node master node-role.kubernetes.io/master:NoSchedule-




- kubeadm init --pod-network-cidr=10.244.0.0/16

1. Create a file called subnet.env at location /run/flannel/ inside your worker nodes.

2. Add the below content in it.
```
FLANNEL_NETWORK=10.244.0.0/16
FLANNEL_SUBNET=10.244.0.1/24
FLANNEL_MTU=1450
FLANNEL_IPMASQ=true
```
3. Save the file and create the pod again. It should saw the runnign status now.


```
- kubectl -n <namespace-name> describe pod <pod name>

kubectl -n <namespace-name> logs -p  <pod name> 
```
