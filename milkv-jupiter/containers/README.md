# 容器
## Docker
### demo简介
#### demo说明
Docker是一个开放源代码的开放平台软件，用于开发应用、交付应用和运行应用。Docker允许用户将基础设施中的应用单独分割出来，形成更小的颗粒（容器），从而提高交付软件的速度。

#### demo源码链接
https://github.com/moby/moby

#### sdk及链接
[官网](https://www.docker.com/)不知道能不能算（？）

#### 环境说明
硬件：Milkv Jupiter

系统：Bianbu 1.0.15 (GNU/Linux 6.1.15 riscv64)

### Demo运行
[Docker](docker.md)

### sdk集成说明
无

### Demo运行总结
安装使用均很方便，支持很好

## Podman
### demo简介
#### demo说明
Podman是红帽公司所推出的一款符合开放源代码容器倡议（OCI）的开放源代码容器管理工具。Podman基于libpod库提供容器、pod、镜像与卷的生命周期管理应用程序接口。

#### demo源码链接
https://github.com/containers/podman

#### 环境说明
硬件：Milkv Jupiter

系统：Bianbu 2.0 (GNU/Linux 6.6.36 riscv64)

### Demo运行
[podman](podman.md)

### Demo运行总结
#### 问题及状态
##### 安装报错
安装会报错缺少一些蓝牙的固件，但目前使用时未发现有问题（可能因为没有调用到这些硬件）

<details>

```
update-initramfs: Generating /boot/initrd.img-6.6.36
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852cu_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852cu_fw_v2.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852cu_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852bu_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852bu_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852bs_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852bs_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852au_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8852au_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8851bu_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8851bu_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8822cu_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8822cu_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8822cs_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8822cs_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8822b_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8822b_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8821cs_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8821cs_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8821c_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8821c_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8821a_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8821a_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8761bu_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8761bu_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8761b_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8761b_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8761a_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8761a_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723ds_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723ds_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723d_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723d_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723cs_xx_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723cs_xx_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723cs_vf_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723cs_vf_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723cs_cg_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723cs_cg_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723bs_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723bs_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723b_config.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723b_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/rtl_bt/rtl8723a_fw.bin for built-in driver btrtl
W: Possible missing firmware /lib/firmware/regulatory.db for built-in driver cfg80211
W: Possible missing firmware /lib/firmware/regulatory.db.p7s for built-in driver cfg80211
```

</details>
