# Lab 3 Submission

## Task 1: First GitHub Actions Workflow

### 1.1 Quickstart Implementation
I created the folder `.github/workflows` and added the `github-actions-demo.yml` file following the official Quickstart guide.

**Key Concepts:**
* **Workflow:** An automated process defined in YAML.
* **Job:** A set of steps that execute on the same runner.
* **Step:** An individual task (command or action).
* **Runner:** A server (e.g., ubuntu-latest) that runs the workflow.

### 1.2 Workflow Trigger & Logs
After pushing the commit, the workflow triggered automatically because of `on: [push]`.

**Evidence:**
* **Link to successful run:** https://github.com/Impuls3gg/DevOps-Intro/actions/runs/22188458164
* **Observations:** I saw the logs printing the branch name, repository name, and listing files.

---

## Task 2: Manual Trigger + System Information

### 2.1 & 2.2 Manual Trigger
I modified the YAML file to include `workflow_dispatch:`. This allowed me to manually trigger the workflow from the "Actions" tab.

**Comparison:**
* **Push:** Triggers automatically on code change. Good for CI tests.
* **Workflow Dispatch:** Triggers only when I click the button. Good for manual deployments or specific tasks.

### 2.3 System Information
I added commands like `lscpu`, `free -h`, and `cat /etc/os-release` to inspect the runner.

**Gathered System Info:**
OS Details:
PRETTY_NAME="Ubuntu 24.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.3 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
--------------------------------
CPU Info:
Architecture:                            x86_64
CPU op-mode(s):                          32-bit, 64-bit
Address sizes:                           48 bits physical, 48 bits virtual
Byte Order:                              Little Endian
CPU(s):                                  4
On-line CPU(s) list:                     0-3
Vendor ID:                               AuthenticAMD
Model name:                              AMD EPYC 7763 64-Core Processor
CPU family:                              25
Model:                                   1
Thread(s) per core:                      2
Core(s) per socket:                      2
Socket(s):                               1
Stepping:                                1
BogoMIPS:                                4890.85
Flags:                                   fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl tsc_reliable nonstop_tsc cpuid extd_apicid aperfmperf tsc_known_freq pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm cmp_legacy svm cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw topoext vmmcall fsgsbase bmi1 avx2 smep bmi2 erms invpcid rdseed adx smap clflushopt clwb sha_ni xsaveopt xsavec xgetbv1 xsaves user_shstk clzero xsaveerptr rdpru arat npt nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold v_vmsave_vmload umip vaes vpclmulqdq rdpid fsrm
Virtualization:                          AMD-V
Hypervisor vendor:                       Microsoft
Virtualization type:                     full
L1d cache:                               64 KiB (2 instances)
L1i cache:                               64 KiB (2 instances)
L2 cache:                                1 MiB (2 instances)
L3 cache:                                32 MiB (1 instance)
NUMA node(s):                            1
NUMA node0 CPU(s):                       0-3
Vulnerability Gather data sampling:      Not affected
Vulnerability Ghostwrite:                Not affected
Vulnerability Indirect target selection: Not affected
Vulnerability Itlb multihit:             Not affected
Vulnerability L1tf:                      Not affected
Vulnerability Mds:                       Not affected
Vulnerability Meltdown:                  Not affected
Vulnerability Mmio stale data:           Not affected
Vulnerability Reg file data sampling:    Not affected
Vulnerability Retbleed:                  Not affected
Vulnerability Spec rstack overflow:      Vulnerable: Safe RET, no microcode
Vulnerability Spec store bypass:         Vulnerable
Vulnerability Spectre v1:                Mitigation; usercopy/swapgs barriers and __user pointer sanitization
Vulnerability Spectre v2:                Mitigation; Retpolines; STIBP disabled; RSB filling; PBRSB-eIBRS Not affected; BHI Not affected
Vulnerability Srbds:                     Not affected
Vulnerability Tsa:                       Vulnerable: Clear CPU buffers attempted, no microcode
Vulnerability Tsx async abort:           Not affected
Vulnerability Vmscape:                   Not affected
--------------------------------
Memory Info:
               total        used        free      shared  buff/cache   available
Mem:            15Gi       1.1Gi       9.0Gi        37Mi       5.9Gi        14Gi
Swap:          4.0Gi          0B      


 4.0Gi

**Evidence:**
* **Link to manual run:**  https://github.com/Impuls3gg/DevOps-Intro/actions/runs/22188985553