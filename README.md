# KinD-handon

* CentOS 8 : Linux version 4.18.0-373.el8.x86_64
* KinD : kind version 0.12.0
* K8s : Kubernetes v1.23.5


### Installing KinD From Release Binaries
[Ref](https://kind.sigs.k8s.io/docs/user/quick-start/#installing-from-release-binaries)

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.12.0/kind-linux-amd64
chmod +x ./kind
mv ./kind /usr/local/bin/kind
```

### Installing kubeadm
[Ref](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)
### Install and Set Up kubectl on Linux
[Ref](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)


### Build the CNI plugins

```bash
# Build in golang container

# Run container
docker run -it -d --name go-build-cni-env -v /home/KinD/CNIplugin:/usr/src/myapp -w /usr/src/myapp golang

# Into container
docker exec -it go-build-env bash

# Get CNI plugin source code
container# git clone https://github.com/containernetworking/plugins.git
container# cd plugins
# this will build the CNI binaries in bin/*
container# ./build_linux.sh
# exit container
container# exit

```

> Node: Must to add extraMounts to mount CNI plugin binary file

### Create KinD cluster
```bash
kind create cluster --config /home/KinD/kind.yaml
```

### Deploying flannel manually
```bash
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
```

