# Docker
当前Docker Hub上已有一些支持riscv64的镜像[^1]，但Docker Engine暂时没有risc-v官方预编译包[^2]，需要自行编译

[^1]: https://hub.docker.com/u/riscv64

[^2]: https://docs.docker.com/engine/install/#supported-platforms

## 安装依赖
``` bash
sudo apt install -y pkg-config libseccomp2 libseccomp-dev runc crun containerd
```

## 安装go
可直接使用apt安装

``` bash
sudo apt install -y golang-go
mkdir -p ~/gopath
echo 'export GOPATH=~/gopath' >> ~/.bashrc
source ~/.bashrc
```

安装完成后直接在命令行中输入go，应该会输出`Go is a tool for managing Go source code.`，以及它的帮助信息

## 编译并安装docker-cli
``` bash
mkdir -p $GOPATH/src/github.com/docker/
cd $GOPATH/src/github.com/docker/
git clone https://github.com/docker/cli
cd cli
DISABLE_WARN_OUTSIDE_CONTAINER=1 GO111MODULE=off make
sudo cp ./build/docker-linux-riscv64 /usr/local/bin
sudo ln -sf /usr/local/bin/docker-linux-riscv64 /usr/local/bin/docker
```

参考：https://github.com/carlosedp/riscv-bringup/