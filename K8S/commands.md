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

```
SQL Server 2019 will run as non-root by default.
This container is running as user mssql.
To learn more visit https://go.microsoft.com/fwlink/?linkid=2099216.
/opt/mssql/bin/sqlservr: Error: The system directory [/.system] could not be created. File: LinuxDirectory.cpp:420 [Status: 0xC0000022 Access Denied errno = 0xD(13) Permission denied]
```

https://github.com/microsoft/mssql-docker/issues/615


chmod 777 test



Namespace:
---

- Создадим неймспейс:

kubectl create namespace msvc-ns


- Установим его как текущий:

kubectl config set-context --current --namespace=msvc-ns

