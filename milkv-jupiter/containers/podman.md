# Podman
## 安装
bianbu系统自带软件源中含有该包，可以直接安装

``` bash
sudo apt install -y podman
```

<details>
<summary>日志</summary>
```
stydxm@milkv-jupiter:~$ sudo apt install -y podman
正在读取软件包列表... 完成
正在分析软件包的依赖关系树... 完成
正在读取状态信息... 完成                 
将会同时安装下列软件：
  buildah catatonit conmon crun fuse-overlayfs fuse3 golang-github-containers-common
  golang-github-containers-image libfuse3-3 libgpgme11 libslirp0 libsubid4 libyajl2 netavark slirp4netns
  uidmap
建议安装：
  containers-storage docker-compose iptables
推荐安装：
  aardvark-dns
下列【新】软件包将被安装：
  buildah catatonit conmon crun fuse-overlayfs fuse3 golang-github-containers-common
  golang-github-containers-image libfuse3-3 libgpgme11 libslirp0 libsubid4 libyajl2 netavark podman
  slirp4netns uidmap
升级了 0 个软件包，新安装了 17 个软件包，要卸载 0 个软件包，有 0 个软件包未被升级。
需要下载 20.2 MB 的归档。
解压缩后会消耗 69.5 MB 的额外空间。
您希望继续执行吗？ [Y/n] 
获取:1 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/main riscv64 libfuse3-3 riscv64 3.14.0-4 [82.9 kB]
获取:2 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/main riscv64 fuse3 riscv64 3.14.0-4 [26.5 kB]
获取:3 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/main riscv64 libsubid4 riscv64 1:4.13+dfsg1-1ubuntu1 [70.5 kB]
获取:4 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/main riscv64 uidmap riscv64 1:4.13+dfsg1-1ubuntu1 [43.4 kB]
获取:5 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 netavark riscv64 1.4.0-3 [1,101 kB]
获取:6 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 golang-github-containers-image all 5.23.1-4 [31.7 kB]
获取:7 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 golang-github-containers-common all 0.50.1+ds1-4 [36.3 kB]
获取:8 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/main riscv64 libgpgme11 riscv64 1.18.0-3ubuntu2 [118 kB]
获取:9 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 buildah riscv64 1.28.2+ds1-3build1 [6,235 kB]
获取:10 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 catatonit riscv64 0.1.7-1 [258 kB]
获取:11 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 conmon riscv64 2.1.6+ds1-1 [43.1 kB]
获取:12 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/main riscv64 libyajl2 riscv64 2.1.0-5 [21.0 kB]
获取:13 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 crun riscv64 1.8.5-1 [1,029 kB]
获取:14 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 fuse-overlayfs riscv64 1.10-1 [47.9 kB]
获取:15 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/main riscv64 libslirp0 riscv64 4.7.0-1ubuntu1 [69.2 kB]
获取:16 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 podman riscv64 4.3.1+ds1-8 [10.9 MB]
获取:17 http://archive.spacemit.com/bianbu-ports mantic/snapshots/v1.0.15/universe riscv64 slirp4netns riscv64 1.2.0-1 [40.6 kB]
已下载 20.2 MB，耗时 1秒 (14.5 MB/s)    
正在选中未选择的软件包 libfuse3-3:riscv64。
(正在读取数据库 ... 系统当前共安装有 29515 个文件和目录。)
准备解压 .../00-libfuse3-3_3.14.0-4_riscv64.deb  ...
正在解压 libfuse3-3:riscv64 (3.14.0-4) ...
正在选中未选择的软件包 fuse3。
准备解压 .../01-fuse3_3.14.0-4_riscv64.deb  ...
正在解压 fuse3 (3.14.0-4) ...
正在选中未选择的软件包 libsubid4:riscv64。
准备解压 .../02-libsubid4_1%3a4.13+dfsg1-1ubuntu1_riscv64.deb  ...
正在解压 libsubid4:riscv64 (1:4.13+dfsg1-1ubuntu1) ...
正在选中未选择的软件包 uidmap。
准备解压 .../03-uidmap_1%3a4.13+dfsg1-1ubuntu1_riscv64.deb  ...
正在解压 uidmap (1:4.13+dfsg1-1ubuntu1) ...
正在选中未选择的软件包 netavark。
准备解压 .../04-netavark_1.4.0-3_riscv64.deb  ...
正在解压 netavark (1.4.0-3) ...
正在选中未选择的软件包 golang-github-containers-image。
准备解压 .../05-golang-github-containers-image_5.23.1-4_all.deb  ...
正在解压 golang-github-containers-image (5.23.1-4) ...
正在选中未选择的软件包 golang-github-containers-common。
准备解压 .../06-golang-github-containers-common_0.50.1+ds1-4_all.deb  ...
正在解压 golang-github-containers-common (0.50.1+ds1-4) ...
正在选中未选择的软件包 libgpgme11:riscv64。
准备解压 .../07-libgpgme11_1.18.0-3ubuntu2_riscv64.deb  ...
正在解压 libgpgme11:riscv64 (1.18.0-3ubuntu2) ...
正在选中未选择的软件包 buildah。
准备解压 .../08-buildah_1.28.2+ds1-3build1_riscv64.deb  ...
正在解压 buildah (1.28.2+ds1-3build1) ...
正在选中未选择的软件包 catatonit。
准备解压 .../09-catatonit_0.1.7-1_riscv64.deb  ...
正在解压 catatonit (0.1.7-1) ...
正在选中未选择的软件包 conmon。
准备解压 .../10-conmon_2.1.6+ds1-1_riscv64.deb  ...
正在解压 conmon (2.1.6+ds1-1) ...
正在选中未选择的软件包 libyajl2:riscv64。
准备解压 .../11-libyajl2_2.1.0-5_riscv64.deb  ...
正在解压 libyajl2:riscv64 (2.1.0-5) ...
正在选中未选择的软件包 crun。
准备解压 .../12-crun_1.8.5-1_riscv64.deb  ...
正在解压 crun (1.8.5-1) ...
正在选中未选择的软件包 fuse-overlayfs。
准备解压 .../13-fuse-overlayfs_1.10-1_riscv64.deb  ...
正在解压 fuse-overlayfs (1.10-1) ...
正在选中未选择的软件包 libslirp0:riscv64。
准备解压 .../14-libslirp0_4.7.0-1ubuntu1_riscv64.deb  ...
正在解压 libslirp0:riscv64 (4.7.0-1ubuntu1) ...
正在选中未选择的软件包 podman。
准备解压 .../15-podman_4.3.1+ds1-8_riscv64.deb  ...
正在解压 podman (4.3.1+ds1-8) ...
正在选中未选择的软件包 slirp4netns。
准备解压 .../16-slirp4netns_1.2.0-1_riscv64.deb  ...
正在解压 slirp4netns (1.2.0-1) ...
正在设置 libyajl2:riscv64 (2.1.0-5) ...
正在设置 libgpgme11:riscv64 (1.18.0-3ubuntu2) ...
正在设置 libsubid4:riscv64 (1:4.13+dfsg1-1ubuntu1) ...
正在设置 golang-github-containers-image (5.23.1-4) ...
正在设置 conmon (2.1.6+ds1-1) ...
正在设置 catatonit (0.1.7-1) ...
正在设置 netavark (1.4.0-3) ...
正在设置 libfuse3-3:riscv64 (3.14.0-4) ...
正在设置 libslirp0:riscv64 (4.7.0-1ubuntu1) ...
正在设置 golang-github-containers-common (0.50.1+ds1-4) ...
正在设置 slirp4netns (1.2.0-1) ...
正在设置 crun (1.8.5-1) ...
正在设置 uidmap (1:4.13+dfsg1-1ubuntu1) ...
正在设置 podman (4.3.1+ds1-8) ...
Created symlink /etc/systemd/system/default.target.wants/podman-auto-update.service → /lib/systemd/system/podman-auto-update.service.
Created symlink /etc/systemd/system/timers.target.wants/podman-auto-update.timer → /lib/systemd/system/podman-auto-update.timer.
Created symlink /etc/systemd/system/default.target.wants/podman-restart.service → /lib/systemd/system/podman-restart.service.
Created symlink /etc/systemd/system/default.target.wants/podman.service → /lib/systemd/system/podman.service.
Created symlink /etc/systemd/system/sockets.target.wants/podman.socket → /lib/systemd/system/podman.socket.
正在设置 fuse3 (3.14.0-4) ...
update-initramfs: deferring update (trigger activated)
正在设置 fuse-overlayfs (1.10-1) ...
正在设置 buildah (1.28.2+ds1-3build1) ...
正在处理用于 libc-bin (2.38-1ubuntu6.1-bb4) 的触发器 ...
正在处理用于 initramfs-tools (0.142ubuntu15-bb2) 的触发器 ...
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
</details>

## Hello World
从Docker Hub拉取镜像，并输出内容

``` bash
podman run --rm hello-world
```

## Ubuntu
Docker Hub中有支持riscv64架构的镜像，我们可以输入以下命令来使用

``` bash
podman run --rm -it ubuntu bash
```