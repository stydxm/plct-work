# RevyOS LicheePi4A 测试结果

## 测试平台

硬件：LicheePi4A 16+128

系统：RevyOS 20250526

```bash
debian@revyos-lpi4a:~$ screenfetch
         _,met$$$$$gg.           debian@revyos-lpi4a
      ,g$$$$$$$$$$$$$$$P.        OS: Debian  trixie
    ,g$$P""       """Y$$.".      Kernel: riscv64 Linux 6.6.92-th1520
   ,$$P'              `$$$.      Uptime: 5h 8m
  ',$$P       ,ggs.     `$$b:    Packages: 1281
  `d$$'     ,$P"'   .    $$$     Shell: bash 5.2.32
   $$P      d$'     ,    $$P     Disk: 7.8G / 118G (7%)
   $$:      $$.   -    ,d$$'     CPU: Unknown @ 3x 1.848GHz
   $$\;      Y$b._   _,d$P'      RAM: 556MiB / 15814MiB
   Y$$.    `.`"Y$$$$P"'         
   `$$b      "-.__              
    `Y$$                        
     `Y$$.                      
       `$$b.                    
         `Y$$b.                 
            `"Y$b._             
                `""""
```

编译器信息：

```bash
debian@revyos-lpi4a:~$ gcc -v
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/libexec/gcc/riscv64-linux-gnu/14/lto-wrapper
Target: riscv64-linux-gnu
Configured with: ../src/configure -v --with-pkgversion='Debian 14.2.0-11revyos1' --with-bugurl=file:///usr/share/doc/gcc-14/README.Bugs --enable-languages=c,ada,c++,go,d,fortran,objc,obj-c++,m2,rust --prefix=/usr --with-gcc-major-version-only --program-suffix=-14 --program-prefix=riscv64-linux-gnu- --enable-shared --enable-linker-build-id --libexecdir=/usr/libexec --without-included-gettext --enable-threads=posix --libdir=/usr/lib --enable-nls --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --with-default-libstdcxx-abi=new --enable-libstdcxx-backtrace --enable-gnu-unique-object --disable-libquadmath --disable-libquadmath-support --enable-plugin --enable-default-pie --with-system-zlib --enable-libphobos-checking=release --with-target-system-zlib=auto --enable-objc-gc=auto --enable-multiarch --disable-werror --disable-multilib --with-arch=rv64gc --with-abi=lp64d --enable-checking=release --build=riscv64-linux-gnu --host=riscv64-linux-gnu --target=riscv64-linux-gnu --with-build-config=bootstrap-lto-lean --enable-link-serialization=32
Thread model: posix
Supported LTO compression algorithms: zlib zstd
gcc version 14.2.0 (Debian 14.2.0-11revyos1)
```

## 测试命令

```bash
sudo /opt/ltp/runltp -p -l ./result.log -o ./test.log -g ./result.html
```

这条命令的意思是：

-p：输出人类可读的日志

-l ./result.log：将所有测试结果输出到 `./result.log`

-o ./test.log：将测试过程中的日志输出到 `./test.log`

-g ./result.html：将测试结果输出为 HTML 文件

## 测试结果

等待一段时间，以上命令运行完成后，就可以在`/opt/ltp/output`和`/opt/ltp/results`看到测试结果

```log
Total Tests: 2472
Total Skipped Tests: 340
Total Failures: 61
Kernel Version: 6.6.92-th1520
Machine Architecture: riscv64
Hostname: revyos-lpi4a
```

## 错误分析

|测试用例|错误原因|
|:-:|:-:|
|irqbalance01|TFAIL: Heuristic: Detected 0 irq-cpu pairs have been dissallowed|
|pty05|TCONF: HDLC line discipline not available|
|memcontrol04|TFAIL: Expect: (A/B/C memory.current=22437888) ~= 34603008<br />HINT: You _MAY_ be hit by known kernel failures:<br />Low events in F: https://bugzilla.suse.com/show_bug.cgi?id=1196298|
|cpuset_regression_test|脚本无法运行|
|hugemmap15|TFAIL: icache unclean<br />HINT: You _MAY_ be missing kernel fixes:<br />https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=cbf52afdc0eb|
|hugemmap24|TFAIL: couldn't find 2 free neighbour slices: ENOMEM (12)|
|nm01_sh|脚本无法运行|
|cpuhotplug03|TBROK: CPU1 cannot be onlined|
|cpuhotplug04|TFAIL: Could not offline cpu0|
|rtc02|TFAIL: seconds1 is 45557, seconds2 is 49157<br \>TFAIL: RTC SET TEST|

## 复测通过

- bind06
- bpf_prog04
- bpf_prog05

提示

```log
bpf_common.c:39: TCONF: Hint: check also /proc/sys/kernel/unprivileged_bpf_disabled
bpf_common.c:40: TCONF: bpf() requires CAP_SYS_ADMIN or CAP_BPF on this system: EPERM (1)
```

执行`echo 0 | sudo tee /proc/sys/kernel/unprivileged_bpf_disabled`后复测通过

- bpf_prog06
- bpf_prog07
- close_range01
- connect02
- fsconfig03
- keyctl03
- madvise06
- sendmsg03
- sendto03
- setsockopt05
- setsockopt06
- setsockopt08
- setsockopt09
- setsockopt10
- timerfd_settime02
- wait403
- cfs_bandwidth01
- pty06
- pty07
- hugemmap07
- can_bcm01
- cve-2016-7042
- cve-2016-8655
- cve-2017-2636
- cve-2017-10661
- cve-2017-16939
- cve-2017-17712
- cve-2017-1000112
- cve-2017-1000380
- cve-2018-7566
- cve-2018-9568
- cve-2018-18445
- cve-2018-18559
- cve-2019-8912
- cve-2020-14386
- cve-2020-36557
- cve-2021-3444
- cve-2021-3609
- cve-2021-4204
- cve-2021-22555
- cve-2021-26708
- cve-2021-22600
- cve-2022-23222
- cve-2023-0461
- cve-2023-31248
- cve-2022-0185
- cve-2022-4378
- af_alg07