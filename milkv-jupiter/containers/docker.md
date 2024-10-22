# Docker
当前Docker Hub上已有一些支持riscv64的镜像[^1]，但Docker Engine暂时没有risc-v官方预编译包[^2]，需要自行编译

[^1]: https://hub.docker.com/u/riscv64

[^2]: https://docs.docker.com/engine/install/#supported-platforms

## apt安装
进迭时空提供的软件源中有docker二进制包，可以直接下载

``` bash
sudo apt install docker.io
```

## 编译安装
### 安装编译过程中的依赖
``` bash
sudo apt install -y pkg-config libseccomp2 libseccomp-dev runc crun containerd iptables
```

### go
可直接使用apt安装

``` bash
sudo apt install -y golang-go
mkdir -p ~/gopath
echo 'export GOPATH=~/gopath' >> ~/.bashrc
source ~/.bashrc
```

安装完成后直接在命令行中输入go，应该会输出`Go is a tool for managing Go source code.`，以及它的帮助信息

### docker-cli
``` bash
mkdir -p $GOPATH/src/github.com/docker/ && cd $GOPATH/src/github.com/docker/
git clone https://github.com/docker/cli && cd cli
DISABLE_WARN_OUTSIDE_CONTAINER=1 GO111MODULE=off make
sudo cp ./build/docker-linux-riscv64 /usr/local/bin
sudo ln -sf /usr/local/bin/docker-linux-riscv64 /usr/local/bin/docker
```

不出意外的话，这时候你使用`docker`命令就可以看到帮助信息了

但这时的docker命令还是没有功能的，因为它只是Docker CLI，而真正运行容器的Docker Engine还没有被安装

### docker-init
``` bash
git clone https://github.com/krallin/tini && cd tini
mkdir build && cd build
export CFLAGS="-DPR_SET_CHILD_SUBREAPER=36 -DPR_GET_CHILD_SUBREAPER=37"
cmake .. && make -j
sudo cp tini-static /usr/local/bin/docker-init
```

### docker-proxy
``` bash
mkdir -p $GOPATH/src/github.com/docker/ && cd $GOPATH/src/github.com/docker/
git clone https://github.com/docker/libnetwork/ && cd libnetwork
go install github.com/ishidawataru/sctp@latest  # go get github.com/ishidawataru/sctp
GO111MODULE=off go build ./cmd/proxy
sudo cp proxy /usr/local/bin/docker-proxy
```

### dockerd
当前该项目依赖go>=1.22，需要注意go的版本
``` bash
mkdir -p $GOPATH/src/github.com/docker/ && cd $GOPATH/src/github.com/docker/
git clone https://github.com/moby/moby docker && cd docker
./hack/make.sh binary
sudo cp bundles/binary-daemon/dockerd /usr/local/bin/dockerd
```

### 编写systemd配置文件
```
cat << EOF | sudo tee -a /etc/systemd/system/containerd.service
[Unit]
Description=containerd container runtime
Documentation=https://containerd.io
After=network.target

[Service]
ExecStartPre=-/sbin/modprobe overlay
ExecStart=/usr/local/bin/containerd
KillMode=process
Delegate=yes
LimitNOFILE=1048576
# Having non-zero Limit*s causes performance problems due to accounting overhead
# in the kernel. We recommend using cgroups to do container-local accounting.
LimitNPROC=infinity
LimitCORE=infinity
TasksMax=infinity

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl start containerd
sudo systemctl enable containerd

cat << EOF | sudo tee -a /etc/systemd/system/docker.service
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
BindsTo=containerd.service
After=network-online.target firewalld.service containerd.service
Wants=network-online.target
Requires=docker.socket

[Service]
Type=notify
# the default is not to use systemd for cgroups because the delegate issues still
# exists and systemd currently does not support the cgroup feature set required
# for containers run by docker
ExecStart=/usr/local/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
ExecReload=/bin/kill -s HUP $MAINPID
TimeoutSec=0
RestartSec=2
Restart=always

# Note that StartLimit* options were moved from "Service" to "Unit" in systemd 229.
# Both the old, and new location are accepted by systemd 229 and up, so using the old location
# to make them work for either version of systemd.
StartLimitBurst=3

# Note that StartLimitInterval was renamed to StartLimitIntervalSec in systemd 230.
# Both the old, and new name are accepted by systemd 230 and up, so using the old name to make
# this option work for either version of systemd.
StartLimitInterval=60s

# Having non-zero Limit*s causes performance problems due to accounting overhead
# in the kernel. We recommend using cgroups to do container-local accounting.
LimitNOFILE=infinity
LimitNPROC=infinity
LimitCORE=infinity

# Comment TasksMax if your systemd version does not supports it.
# Only systemd 226 and above support this option.
TasksMax=infinity

# set delegate yes so that systemd does not reset the cgroups of docker containers
Delegate=yes

# kill only the docker process, not all processes in the cgroup
KillMode=process

[Install]
WantedBy=multi-user.target
EOF

cat << EOF | sudo tee -a /etc/systemd/system/docker.socket
[Unit]
Description=Docker Socket for the API

[Socket]
# If /var/run is not implemented as a symlink to /run, you may need to
# specify ListenStream=/var/run/docker.sock instead.
ListenStream=/run/docker.sock
SocketMode=0660
SocketUser=root
SocketGroup=docker

[Install]
WantedBy=sockets.target
EOF

sudo systemctl start docker
sudo systemctl enable docker
```

## 运行Hello World镜像
在命令行中输入

``` bash
sudo docker run --rm hello-world
```

可正常拉取镜像，并输出内容：

```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (riscv64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

## 在容器中运行其他发行版
``` bash
sudo docker run -it --rm ubuntu bash
```

参考：https://github.com/carlosedp/riscv-bringup/
