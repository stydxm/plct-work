# Pytorch
**还未完成，目前编译遇到问题**

## 编译
目前进迭时空的apt软件源中还没有pytorch，而官方的pypi源中也没有支持riscv架构的，因此需要自行编译

参考：https://github.com/pytorch/pytorch#from-source

### 安装编译过程中需要的依赖
``` bash
sudo apt install -y python3 python3-pip python3-venv python3-openssl python3- git cmake ninja-build autoconf rustc cargo
```

### 下载代码
``` bash
git clone --recursive https://github.com/pytorch/pytorch
cd pytorch
```

### 创建虚拟环境并安装依赖
``` bash
python3 -m venv .venv
source .venv/bin/activate
pip3 install -r requirements.txt
```

注意这里有一些依赖项如`numpy`也需要编译，因此安装耗时可能会很长

### 编译并安装
``` bash
export _GLIBCXX_USE_CXX11_ABI=1
python3 setup.py develop
```