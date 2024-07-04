---
description: >-
  https://computingforgeeks.com/how-to-setup-kubernetes-cluster-on-ubuntu-18-04/#google_vignette
---

# One Node Kubernetes

## 기본 설치

```diff
sudo useradd -s /bin/bash -m k8s-admin
sudo passwd k8s-admin
sudo usermod -aG sudo k8s-admin
echo "k8s-admin ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/k8s-admin
```

1.  [docker 설치](https://computingforgeeks.com/how-to-setup-3-node-kubernetes-cluster-on-ubuntu-18-04-with-weave-net-cni/)

    ```diff
    sudo apt-get install \\
    apt-transport-https \\
    ca-certificates \\
    curl \\
    software-properties-common
    ```

    *   Import Docker repository GPG key

        ```diff
        $ curl -fsSL <https://download.docker.com/linux/ubuntu/gpg> | sudo apt-key add -

        $ sudo add-apt-repository \\
         "deb [arch=amd64] <https://download.docker.com/linux/ubuntu> \\
         $(lsb_release -cs) \\
         stable"
        ```

    ```diff
    sudo apt-get update
    sudo apt-get install docker-ce
    sudo adduser k8s-admin docker 
    sudo usermod -aG docker k8s-admin
    ```

    ```diff
    k8s-admin@ecga-OptiPlex-7080:~$ docker info
    Client:
     Context:    default
     Debug Mode: false
     Plugins:
      app: Docker App (Docker Inc., v0.9.1-beta3)
      buildx: Build with BuildKit (Docker Inc., v0.5.1-docker)
      scan: Docker Scan (Docker Inc., v0.7.0)

    Server:
     Containers: 1
      Running: 0
      Paused: 0
      Stopped: 1
     Images: 1
     Server Version: 20.10.6
     Storage Driver: overlay2
      Backing Filesystem: extfs
      Supports d_type: true
      Native Overlay Diff: true
      userxattr: false
     Logging Driver: json-file
     Cgroup Driver: cgroupfs
     Cgroup Version: 1
     Plugins:
      Volume: local
      Network: bridge host ipvlan macvlan null overlay
      Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
     Swarm: inactive
     Runtimes: io.containerd.runtime.v1.linux runc io.containerd.runc.v2
     Default Runtime: runc
     Init Binary: docker-init
     containerd version: 05f951a3781f4f2c1911b05e61c160e9c30eaa8e
     runc version: 12644e614e25b05da6fd08a38ffa0cfe1903fdec
     init version: de40ad0
     Security Options:
      apparmor
      seccomp
       Profile: default
     Kernel Version: 5.8.0-43-generic
     Operating System: Ubuntu 20.04.2 LTS
     OSType: linux
     Architecture: x86_64
     CPUs: 12
     Total Memory: 31.08GiB
     Name: ecga-OptiPlex-7080
     ID: JS7G:MUGZ:RXDX:UZJI:52HQ:DLTU:ROKE:FKKX:KMEX:LDR6:DONU:PY6D
     Docker Root Dir: /var/lib/docker
     Debug Mode: false
     Registry: <https://index.docker.io/v1/>
     Labels:
     Experimental: false
     Insecure Registries:
      127.0.0.0/8
     Live Restore Enabled: false
    ```

    시스템 부팅시에 실행되도록 설정

    ```diff
    sudo systemctl enable docker && service docker start
    ```

    portainer 실행 ( docker gui)

    ```diff
    mkdir -p /data/portainer // 컨테이너와 host(vm)간에 볼륨매칭을 위한 디렉터리 생성부터 진행하겠습니다.
    ```

    ```diff
    sudo docker run --name portainer -p 9000:9000 -d --restart always -v /data/portainer:/data -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
    ```

    [http://123.140.248.213:9000/#/init/admin](http://123.140.248.213:9000/#/init/admin)

    [http://123.140.248.213:9000/#/home](http://123.140.248.213:9000/#/home)

    username: ecga

    password: eccafe24@001

    trouble

    ```diff
    docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create?name=portainer: dial unix /var/run/docker.sock: connect: permission denied.
    See 'docker run --help'.

    // 해당 문제는 사용자가 /var/run/docker.sock 을 접근하려고 하였지만 권한이 없어 발생하는 문제로 사용자가 root:docker 권한을 가지고 있어야 한다.
    srw-rw---- 1 root docker 0  5월 30 21:44 /var/run/docker.sock
    [해결!]
    sudo usermod -a -G docker $USER
    sudo docker run hello-world <-- root로 실행 못하므로~
    ```

    3. kubernetes

    ```diff
    curl -s <https://packages.cloud.google.com/apt/doc/apt-key.gpg> | sudo apt-key add
    ```

    ```diff
    sudo apt-add-repository "deb <http://apt.kubernetes.io/> kubernetes-xenial main"
    ```

    ```diff
    sudo swapoff --all
    sudo hostnamectl set-hostname master-node
    sudo kubeadm reset
    # sudo kubeadm init --pod-network-cidr=10.244.0.0/16
    sudo kubeadm init --apiserver-advertise-address=123.140.248.213 --pod-network-cidr=10.244.0.0/16 --cri-socket /var/run/crio/crio.sock

    "Your Kubernetes control-plane has initialized successfully! "

    kubectl apply -f <https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml>
    kubectl apply -f <https://raw.githubusercontent.com/kubernetes/dashboard/v2.4.0/aio/deploy/recommended.yaml>

    kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
    nohup kubectl port-forward --address='0.0.0.0' -n kubernetes-dashboard service/kubernetes-dashboard 10443:443 &

    kubectl create clusterrolebinding default-cluster-admin --clusterrole cluster-admin --serviceaccount default:default
    ```

    ```diff
    sudo swapoff --all
    sudo hostnamectl set-hostname master-node
    sudo kubeadm reset
    sudo kubeadm init --pod-network-cidr=10.244.0.0/16

    "Your Kubernetes control-plane has initialized successfully! "

    kubectl apply -f <https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml>

    kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
    nohup kubectl port-forward --address='0.0.0.0' -n kubernetes-dashboard service/kubernetes-dashboard 10443:443 &
    ```

    ```diff
    sudo swapoff --all
    sudo hostnamectl set-hostname master-node
    sudo kubeadm reset
    sudo kubeadm init --pod-network-cidr=10.244.0.0/16

    "Your Kubernetes control-plane has initialized successfully! "

    kubectl apply -f <https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml>

    kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
    nohup kubectl port-forward --address='0.0.0.0' -n kubernetes-dashboard service/kubernetes-dashboard 10443:443 &
    ```

## Docker 설치

