# kubedev

![license](https://img.shields.io/hexpm/l/plug.svg)

# Overview
`kubedev` is a development tool which will build kubernetes components. Considering there are already build scripts in kubernetes, `kubedev` will do these additional work:
- Pull build images using China mirror source.
- Write version file and give the component right version automatically.
- Build `Binary`, `Image`, `Rpm`, `Deb`(not supported yet) packages directly.
- Better log handling.

# Quick Start 

Make make sure you have the right Golang development environment:
```shell
export GO111MODULE=on
# For China uses
export GOPROXY="https://goproxy.cn" 
```

Install `kubedev`:
```shell
git clone https://github.com/zhouya0/kubedev.git
cd kubedev
make
make install
```
Going to your kubernetes repo (depending on your own environment):
```shell
cd /root/gopath/src/k8s.io/kubernetes
```

Make sure `rpmbuild` is intalled in your environment:
```shell
yum install rpm-build
```

Start `kubedev`!
```shell
kubedev rpm kubelet
```

See blow info means building is succeed!
```
Using config file: /root/.kubedev.yaml
✔︎ Writing version file 📝
✔︎ Building binary kubelet 🔨
Building binary kubelet success! File can be found in:
 _output/dockerized/bin/linux/amd64/kubelet
✔︎ Packaging binary to RPM 📦
Building RPM kubelet success! Package can be found in:
 /root/rpmbuild/RPMS
```
# Usage

Building binary whith arch arm64:
```shell
kubedev bin kubectl -a armd64
```

Building images with specified repo tag:
```shell
cat <<EOF >> ~/.kubedev.yaml
DockerRegistry: yaopolytech
DockerTag: v1.18.0
EOF
```
Then build `kube-apiserver`, `kube-scheduler`, `kube-proxy`images: 
```shell
kubedev image
```
