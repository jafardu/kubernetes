# kubernetes
k8s学习-搭建-以及服务管理
## k8s安装
bash install ./k8s_install/k8s_install.sh
## 初始化k8s集群
```
kubeadm init --kubernetes-version=v1.15.3 --pod-network-cidr=10.244.0.0/16 --service-cidr=10.96.0.0/12  --image-repository registry.aliyuncs.com/google_containers
```
## 安装coredns flannel
```
#安装coredns
$ ./k8s_install/coredns/deploy.sh | kubectl apply -f -
$ kubectl delete --namespace=kube-system deployment kube-dns
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
#如果不能正常安装，下载yaml文件并修改镜像地址，镜像地址可以使用googlecontainer/flannel-amd64:0.5.5
wget https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
kubectl apply -f  kube-flannel.yml
```
## 配置secret ,使用secret拉去私有镜像仓库镜像
```
kubectl create secret docker-registry myregistrykey --docker-server=DOCKER_REGISTRY_SERVER --docker-username=DOCKER_USER --docker-password=DOCKER_PASSWORD --docker-email=DOCKER_EMAIL -n namespace
```
#### 阿里云的配置方式
$ kubectl create secret docker-registry  web --docker-server=https://registry.cn-shenzhen.aliyuncs.com   --docker-username=yundv  --docker-password=password --docker-email=yundv@outlook.com -n qqb
## ingress-nginx安装
https://github.com/yundd/kubernetes/blob/master/k8s_install/ingress/ingress.md
