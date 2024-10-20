# 容器
## Docker
### demo简介
#### demo说明
Docker是一个开放源代码的开放平台软件，用于开发应用、交付应用和运行应用。Docker允许用户将基础设施中的应用单独分割出来，形成更小的颗粒（容器），从而提高交付软件的速度。

#### demo源码链接
https://github.com/moby/moby

#### 环境说明
硬件：Milkv Jupiter

系统：Bianbu 1.0.15 (GNU/Linux 6.1.15 riscv64)

### Demo运行
[demo运行](docker.md)

### Demo运行总结
需要自行编译，步骤较繁琐，耗时长

## Podman
### demo简介
#### demo说明
Podman是红帽公司所推出的一款符合开放源代码容器倡议（OCI）的开放源代码容器管理工具。Podman基于libpod库提供容器、pod、镜像与卷的生命周期管理应用程序接口。

#### demo源码链接
https://github.com/containers/podman

#### 环境说明
硬件：Milkv Jupiter

系统：Bianbu 1.0.15 (GNU/Linux 6.1.15 riscv64)

### Demo运行
[demo运行](podman.md)

### Demo运行总结
#### 问题及状态
##### 安装报错
```
update-initramfs: Generating /boot/initrd.img-6.1.15
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852cu_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852cu_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852bu_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852bu_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852au_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852au_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8822b_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8822b_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8821a_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8821a_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8761a_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8761a_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723ds_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723ds_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723bs_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723bs_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723b_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723b_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723a_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/regulatory.db for built-in driver cfg80211
W: Possible missing firmware /lib/firmware/regulatory.db.p7s for built-in driver cfg80211
```

##### 普通用户启动容器失败
使用Podman启动容器，会报错找不到tun
```
Error: /usr/bin/slirp4netns failed: "open(\"/dev/net/tun\"): No such file or directory\nWARNING: Support for seccomp is experimental\nWARNING: Support for IPv6 is experimental\nchild failed(1)\nWARNING: Support for seccomp is experimental\nWARNING: Support for IPv6 is experimental\n"
```

若尝试用modprobe加载，也会报错：

```
modprobe: FATAL: Module tun not found in directory /lib/modules/6.1.15
```

用`find /lib/modules/ | grep tun`命令查看，确实没有该模块（在我的x86 arch机器上，能找到`kernel/drivers/net/tun.ko.zst`）

##### 管理员用户启动容器失败
使用sudo权限，则会由netavark报错，怀疑问题还是出在tun
```
Error: netavark: No such file or directory (os error 2)
```