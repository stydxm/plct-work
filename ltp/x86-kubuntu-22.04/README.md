# KUbuntu 22.04 x86测试结果

## 测试平台

机械革命无界15X

```bash
stydxm@stydxm-WUJIE15XA:~$ screenfetch
                          ./+o+-       stydxm@stydxm-WUJIE15XA
                  yyyyy- -yyyyyy+      OS: Ubuntu 22.04 jammy
               ://+//////-yyyyyyo      Kernel: x86_64 Linux 6.8.0-60-generic
           .++ .:/++++++/-.+sss/`      Uptime: 2d 8h 33m
         .:++o:  /++++++++/:--:/-      Packages: 3969
        o:+o+:++.`..```.-/oo+++++/     Shell: bash 5.1.16
       .:+o:+o/.          `+sssoo+/    Resolution: 6000x1600
  .++/+:+oo+o:`             /sssooo.   DE: KDE 5.92.0 / Plasma 5.24.7
 /+++//+:`oo+o               /::--:.   WM: KWin
 \+/+o+++`o++o               ++////.   GTK Theme: Breeze [GTK2/3]
  .++.o+++oo+:`             /dddhhh.   Icon Theme: breeze
       .+.o+oo:.          `oddhhhh+    Disk: 254G / 469G (58%)
        \+.++o+o``-````.:ohdhhhhh+     CPU: AMD Ryzen 7 8845HS w/ Radeon 780M Graphics @ 16x 5.1GHz
         `:o+++ `ohhhhhhhhyo++os:      GPU: AMD Radeon Graphics (radeonsi, gfx1103_r1, LLVM 19.1.2, DRM 3.59, 6.8.0-60-generic)
           .o:`.syhhhhhhh/.oo++o`      RAM: 8467MiB / 23311MiB
               /osyyyyyyo++ooo+++/    
                   ````` +oo+++o\:    
                          `oo++.
```

编译器信息：

```bash
stydxm@stydxm-WUJIE15XA:~$ gcc -v
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/lib/gcc/x86_64-linux-gnu/11/lto-wrapper
OFFLOAD_TARGET_NAMES=nvptx-none:amdgcn-amdhsa
OFFLOAD_TARGET_DEFAULT=1
Target: x86_64-linux-gnu
Configured with: ../src/configure -v --with-pkgversion='Ubuntu 11.4.0-1ubuntu1~22.04' --with-bugurl=file:///usr/share/doc/gcc-11/README.Bugs --enable-languages=c,ada,c++,go,brig,d,fortran,objc,obj-c++,m2 --prefix=/usr --with-gcc-major-version-only --program-suffix=-11 --program-prefix=x86_64-linux-gnu- --enable-shared --enable-linker-build-id --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --libdir=/usr/lib --enable-nls --enable-bootstrap --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --with-default-libstdcxx-abi=new --enable-gnu-unique-object --disable-vtable-verify --enable-plugin --enable-default-pie --with-system-zlib --enable-libphobos-checking=release --with-target-system-zlib=auto --enable-objc-gc=auto --enable-multiarch --disable-werror --enable-cet --with-arch-32=i686 --with-abi=m64 --with-multilib-list=m32,m64,mx32 --enable-multilib --with-tune=generic --enable-offload-targets=nvptx-none=/build/gcc-11-XeT9lY/gcc-11-11.4.0/debian/tmp-nvptx/usr,amdgcn-amdhsa=/build/gcc-11-XeT9lY/gcc-11-11.4.0/debian/tmp-gcn/usr --without-cuda-driver --enable-checking=release --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=x86_64-linux-gnu --with-build-config=bootstrap-lto-lean --enable-link-serialization=2
Thread model: posix
Supported LTO compression algorithms: zlib zstd
gcc version 11.4.0 (Ubuntu 11.4.0-1ubuntu1~22.04) 
```

## 测试命令

```bash
sudo /opt/ltp/runltp -p -l ./result.log -o ./test.log -g ./result.html -C ./
```

这条命令的意思是：

-p：输出人类可读的日志

-l ./result.log：将所有测试结果输出到 `./result.log`

-o ./test.log：将测试过程中的日志输出到 `./test.log`

-g ./result.html：将测试结果输出为 HTML 文件

-C ./：将以上所有文件放在当前目录下

## 测试结果

等待一段时间，以上命令运行完成后，就可以在`/opt/ltp/output`和`/opt/ltp/results`看到测试结果

```log
Total Tests: 2472
Total Skipped Tests: 249
Total Failures: 27
```

具体项目及原因可查看日志
