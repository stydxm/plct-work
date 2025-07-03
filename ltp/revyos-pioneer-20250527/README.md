# RevyOS Pioneer 测试结果

## 测试平台

硬件：Milk-V Pioneer

系统：RevyOS 20250527-225806

```bash
         _,met$$$$$gg.           debian@revyos-upstream
      ,g$$$$$$$$$$$$$$$P.        OS: Debian 
    ,g$$P""       """Y$$.".      Kernel: riscv64 Linux 6.15.1-pioneer
   ,$$P'              `$$$.      Uptime: 33m
  ',$$P       ,ggs.     `$$b:    Packages: 1200
  `d$$'     ,$P"'   .    $$$     Shell: bash 5.2.37
   $$P      d$'     ,    $$P     Disk: 16G / 1002G (2%)
   $$:      $$.   -    ,d$$'     CPU: 64x Unknown
   $$\;      Y$b._   _,d$P'      GPU: Advanced Micro Devices, Inc. [AMD/ATI] Caicos [Radeon HD 6450/7450/8450 / R5 230 OEM]
   Y$$.    `.`"Y$$$$P"'          RAM: 1654MiB / 127874MiB
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
debian@revyos-upstream:~$ gcc -v
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/libexec/gcc/riscv64-linux-gnu/14/lto-wrapper
Target: riscv64-linux-gnu
Configured with: ../src/configure -v --with-pkgversion='Debian 14.2.0-14revyos1' --with-bugurl=file:///usr/share/doc/gcc-14/README.Bugs --enable-languages=c,ada,c++,go,d,fortran,objc,obj-c++,m2,rust --prefix=/usr --with-gcc-major-version-only --program-suffix=-14 --program-prefix=riscv64-linux-gnu- --enable-shared --enable-linker-build-id --libexecdir=/usr/libexec --without-included-gettext --enable-threads=posix --libdir=/usr/lib --enable-nls --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --with-default-libstdcxx-abi=new --enable-libstdcxx-backtrace --enable-gnu-unique-object --disable-libquadmath --disable-libquadmath-support --enable-plugin --enable-default-pie --with-system-zlib --enable-libphobos-checking=release --with-target-system-zlib=auto --enable-objc-gc=auto --enable-multiarch --disable-werror --disable-multilib --with-arch=rv64gc --with-abi=lp64d --enable-checking=release --build=riscv64-linux-gnu --host=riscv64-linux-gnu --target=riscv64-linux-gnu --with-build-config=bootstrap-lto-lean --enable-link-serialization=32
Thread model: posix
Supported LTO compression algorithms: zlib zstd
gcc version 14.2.0 (Debian 14.2.0-14revyos1) 
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
Total Skipped Tests: 292
Total Failures: 38
Kernel Version: 6.15.1-pioneer
Machine Architecture: riscv64
Hostname: revyos-upstream
```

## 错误分析

|测试用例|错误原因|
|:-:|:-:|
|leapsec01|TBROK: adjtimex status 8208 not set|
|clock_settime03|超时时间设为100倍（3000s）后仍超时|
|overcommit_memory01|TINFO: malloc 261887544 kB failed<br /> TFAIL: alloc failed, expected to pass|
|overcommit_memory03|TINFO: malloc 261887544 kB failed<br /> TFAIL: alloc failed, expected to pass|
|overcommit_memory04|TINFO: malloc 261887544 kB failed<br /> TFAIL: alloc failed, expected to pass|
|overcommit_memory05|TINFO: malloc 261887544 kB failed<br /> TFAIL: alloc failed, expected to pass|
|overcommit_memory06|TINFO: malloc 261887544 kB failed<br /> TFAIL: alloc failed, expected to pass|
|irqbalance01|TFAIL: Heuristic: Detected 0 irq-cpu pairs have been dissallowed|
|cgroup|脚本无法运行|
|cgroup_fj_*|脚本无法运行|
|hugemmap15|TFAIL: icache unclean<br />HINT: You _MAY_ be missing kernel fixes:<br />https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=cbf52afdc0eb|
|hugemmap24|hugemmap24.c:62: TINFO: can't use slice_boundary: 0x20000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0x30000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0x40000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0x50000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0x60000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0x70000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0x80000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0x90000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0xa0000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0xb0000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0xc0000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0xd0000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0xe0000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0xf0000000000: ENOMEM (12)<br />hugemmap24.c:62: TINFO: can't use slice_boundary: 0x100000000000: ENOMEM (12)<br />hugemmap24.c:71: TFAIL: couldn't find 2 free neighbour slices: ENOMEM (12)|
|nm01_sh|脚本无法运行|

## 复测通过

部分测试用例超时，将`LTP_TIMEOUT_MUL`设为10后通过

- clock_nanosleep02
- ksm01_1
- ksm02
- ksm02_1
- ksm03
- ksm03_1
- ksm04
- ksm04_1