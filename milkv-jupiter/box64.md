## demo简介
### demo说明
box64是一个Linux 用户空间的 x86_64 模拟器。

### demo源码链接
https://github.com/ptitSeb/box64

### sdk及链接
无

### 环境说明
硬件：Milkv Jupiter

系统：Bianbu 2.0 (GNU/Linux 6.6.36 riscv64)

## Demo运行

### 编译

``` bash
git clone https://github.com/ptitSeb/box64 && cd box64
mkdir build && cd build
cmake .. -D RV64=1 -D CMAKE_BUILD_TYPE=RelWithDebInfo
make -j && sudo make install
```

### 运行

假设要运行的二进制文件为`exe`，则可输入`box64`执行

## Demo运行总结
### sdk集成说明

### 问题及状态
