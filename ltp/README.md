# Linux Test Project
## 介绍

Linux Test Project是由SGI、OSDL和Bull联合启动，由SUSE、Red Hat、Fujitsu、IBM、Cisco、Oracle等共同开发和维护的项目。该项目的目标是向开源社区提供测试，以验证Linux内核的可靠性、鲁棒性和稳定性。

测试套件包含了一组用于测试Linux内核和相关特性的工具。我们的目标是通过引入测试自动化来改进Linux内核和系统库。

## 链接

文档：http://linux-test-project.rtfd.io/

源码：https://github.com/linux-test-project/ltp

邮件列表：http://lists.linux.it/listinfo/ltp

## 环境

安装依赖

```bash
sudo apt install git autoconf automake make gcc m4 pkg-config
```

## 编译安装

```bash
git clone --recurse-submodules https://github.com/linux-test-project/ltp.git
cd ltp
git checkout 20250530
make autotools
./configure
make -j$(nproc)
sudo make install
```

## 运行

为了统一测试内容，在编译前将git设置到tag为20250530的提交

### Kirk

LTP使用一个叫 [Kirk](https://github.com/linux-test-project/kirk) 的工具运行，在 `make install` 时它也会被一同安装到 `/opt/ltp/kirk`，它的用法可参考文档或使用 `-h` 查看

例如，运行 `syscalls` 测试套件可使用

```bash
/opt/ltp/kirk --framework ltp --run-suite syscalls
```

注意，一些测试项目可能会需要root权限，例如测试结果中错误原因是 Permission Deniee 的，可使用 sudo 运行

开始运行前 kirk 会打印出如下的系统信息

```log
Host information

        System: Linux
        Node: revyos-lpi4a
        Kernel Release: 6.6.92-th1520
        Kernel Version: #2025.05.26.14.02+c9a17b235 SMP Mon May 26 14:22:33 UTC 2025
        Machine Architecture: riscv64
        Processor: 

        Temporary directory: /tmp/kirk.root/tmp99hl5v44

Connecting to SUT: host
```

测试的log和结果将会被保存 在`/tmp/kirk.root/tmpxxxx` 中可供查看

### runltp

虽然现在 Kirk 是推荐的运行 LTP 的方式，但它有明显不足：不能一次运行所有测试项目，每次只能运行一个测试套件，而它的测试套件数量非常多，手动运行并整理结果非常麻烦，因此我们还是选择使用更老的 runltp 来运行测试
