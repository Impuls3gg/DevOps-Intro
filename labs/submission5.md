# Lab 5: Virtualization & System Analysis

## Task 1 — VirtualBox Installation

* **Host Operating System:** Windows 11 Pro 23H2
* **VirtualBox Version:** 7.2.6 r172322 (Qt6.8.0 on windows)   
* **Installation Issues:** There were no problems
---

## Task 2 — Ubuntu VM and System Analysis

### VM Configuration
* **OS:** Ubuntu 24.04 LTS
* **RAM:** 4096 MB
* **Storage:** 25 GB
* **CPU Cores:** 2 cores

### System Information Discovery

#### 1. CPU Details
* **Command used:** `lscpu`
* **Output:**
```text
Architecture:                x86_64
  CPU op-mode(s):            32-bit, 64-bit
  Address sizes:             48 bits physical, 48 bits virtual
  Byte Order:                Little Endian
CPU(s):                      2
  On-line CPU(s) list:       0,1
Vendor ID:                   AuthenticAMD
  Model name:                AMD Ryzen 5 1600 Six-Core Processor
    CPU family:              23
    Model:                   1
    Thread(s) per core:      1
    Core(s) per socket:      2
    Socket(s):               1
    Stepping:                1
    BogoMIPS:                6388.11
    Flags:                   fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pg
                             e mca cmov pat pse36 clflush mmx fxsr sse sse2 ht s
                             yscall nx mmxext fxsr_opt rdtscp lm constant_tsc re
                             p_good nopl nonstop_tsc cpuid extd_apicid tsc_known
                             _freq pni pclmulqdq ssse3 fma cx16 sse4_1 sse4_2 mo
                             vbe popcnt aes xsave avx f16c rdrand hypervisor lah
                             f_lm cmp_legacy cr8_legacy abm sse4a misalignsse 3d
                             nowprefetch ssbd vmmcall fsgsbase bmi1 avx2 bmi2 rd
                             seed adx clflushopt sha_ni arat
Virtualization features:     
  Hypervisor vendor:         KVM
  Virtualization type:       full
Caches (sum of all):         
  L1d:                       64 KiB (2 instances)
  L1i:                       128 KiB (2 instances)
  L2:                        1 MiB (2 instances)
  L3:                        32 MiB (2 instances)
NUMA:                        
  NUMA node(s):              1
  NUMA node0 CPU(s):         0,1
Vulnerabilities:             
  Gather data sampling:      Not affected
  Ghostwrite:                Not affected
  Indirect target selection: Not affected
  Itlb multihit:             Not affected
  L1tf:                      Not affected
  Mds:                       Not affected
  Meltdown:                  Not affected
  Mmio stale data:           Not affected
  Old microcode:             Not affected
  Reg file data sampling:    Not affected
  Retbleed:                  Mitigation; untrained return thunk; SMT disabled
  Spec rstack overflow:      Mitigation; SMT disabled
  Spec store bypass:         Not affected
  Spectre v1:                Mitigation; usercopy/swapgs barriers and __user poi
                             nter sanitization
  Spectre v2:                Mitigation; Retpolines; STIBP disabled; RSB filling
                             ; PBRSB-eIBRS Not affected; BHI Not affected
  Srbds:                     Not affected
  Tsa:                       Not affected
  Tsx async abort:           Not affected
  Vmscape:                   Not affected
```

#### 2. Memory Information
* **Command used:** `free -h`
* **Output:**
```text
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       2.1Gi       101Mi       624Mi       2.5Gi       1.7Gi
Swap:             0B          0B          0B
```

#### 3. Network Configuration
* **Command used:** `ip a`
* **Output:**
```text
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:0a:3a:4f brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86133sec preferred_lft 86133sec
    inet6 fd17:625c:f037:2:3618:2a68:c0dd:8db5/64 scope global temporary dynamic 
       valid_lft 86134sec preferred_lft 14134sec
    inet6 fd17:625c:f037:2:a00:27ff:fe0a:3a4f/64 scope global dynamic mngtmpaddr 
       valid_lft 86134sec preferred_lft 14134sec
    inet6 fe80::a00:27ff:fe0a:3a4f/64 scope link 
       valid_lft forever preferred_lft forever
```

#### 4. Storage Information
* **Command used:** `df -h`
* **Output:**
```text
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           392M  1.9M  390M   1% /run
/dev/sr0        6.2G  6.2G     0 100% /cdrom
/cow            2.0G  226M  1.7G  12% /
tmpfs           2.0G  8.0K  2.0G   1% /dev/shm
tmpfs           5.0M  8.0K  5.0M   1% /run/lock
tmpfs           2.0G  386M  1.6G  20% /tmp
tmpfs           392M  160K  392M   1% /run/user/1000
/dev/sda2        25G  2.0G   22G   9% /target
```

#### 5. Operating System & Kernel
* **Command used:** `cat /etc/os-release && uname -a`
* **Output:**
```text
PRETTY_NAME="Ubuntu 24.04.4 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.4 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
Linux ubuntu 6.17.0-14-generic #14~24.04.1-Ubuntu SMP PREEMPT_DYNAMIC Thu Jan 15 15:52:10 UTC 2 x86_64 x86_64 x86_64 GNU/Linux
```


#### 6. Virtualization Detection
* **Command used:** `systemd-detect-virt`
* **Output:**
```text
    oracle
```

