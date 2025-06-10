# RevyOS LicheePi4A 测试结果

由于目标平台性能不足，故将超时时长从默认的 1h 提升至了 100h

## syscalls

```bash
sudo /opt/ltp/kirk --framework ltp --run-suite syscalls --suite-timeout 100h

```

```log
Execution time: 1h 1m 0s

Suite Name: syscalls
Total Run: 1473
Total Runtime: 59m 47s
Passed Tests: 14165
Failed Tests: 0
Skipped Tests: 603
Broken Tests: 0
Warnings: 0
Kernel Version: Linux 6.6.92-th1520 #2025.05.26.14.02+c9a17b235 SMP Mon May 26 14:22:33 UTC 2025
CPU: unknown
Machine Architecture: riscv64
RAM: 16194368 kB
Swap memory: 4194300 kB
Distro: debian
Distro Version: 
```

## commands

```bash
sudo /opt/ltp/kirk --framework ltp --run-suite commands --suite-timeout 100h

```

```log
Execution time: 40.786s

Suite Name: commands
Total Run: 36
Total Runtime: 38.958s
Passed Tests: 292
Failed Tests: 0
Skipped Tests: 17
Broken Tests: 1
Warnings: 0
Kernel Version: Linux 6.6.92-th1520 #2025.05.26.14.02+c9a17b235 SMP Mon May 26 14:22:33 UTC 2025
CPU: unknown
Machine Architecture: riscv64
RAM: 16194368 kB
Swap memory: 4194300 kB
Distro: debian
Distro Version:
```


## containers

```bash
sudo /opt/ltp/kirk --framework ltp --run-suite containers --suite-timeout 100h

```

```log
Execution time: 40.600s

Suite Name: containers
Total Run: 84
Total Runtime: 36.557s
Passed Tests: 230
Failed Tests: 0
Skipped Tests: 2
Broken Tests: 0
Warnings: 0
Kernel Version: Linux 6.6.92-th1520 #2025.05.26.14.02+c9a17b235 SMP Mon May 26 14:22:33 UTC 2025
CPU: unknown
Machine Architecture: riscv64
RAM: 16194368 kB
Swap memory: 4194300 kB
Distro: debian
Distro Version: 


Disconnecting from SUT: host
Session stopped
```

