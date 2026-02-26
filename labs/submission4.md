# Lab 4 — Operating Systems & Networking

## Task 1 — Operating System Analysis

### 1.1 Boot Performance Analysis

**System boot time:**

```
Startup finished in 1.395s (userspace)
graphical.target reached after 1.352s in userspace.
```

**Top 5 slowest services:**

```
628ms landscape-client.service
338ms dev-sdd.device
259ms snapd.seeded.service
179ms systemd-udev-trigger.service
178ms user@1000.service
```

**System load:**

```
 18:23:11 up 5 min,  1 user,  load average: 0.17, 0.14, 0.07
```

```
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU  WHAT
user     pts/1    -                18:18    4:47   0.03s  0.02s -bash
```

**Observations:**
- Boot completed in ~1.4s (userspace only, no kernel phase — WSL environment).
- `landscape-client.service` is the slowest service (628ms), nearly half the total boot time.
- System load is very low (0.17) — the machine is mostly idle.

---

### 1.2 Process Forensics

**Top processes by memory:**

```
    PID    PPID CMD                         %MEM %CPU
    212       1 /usr/bin/python3 /usr/share  0.2  0.0
   1975       1 /usr/libexec/packagekitd     0.2  0.0
     52       1 /usr/lib/systemd/systemd-jo  0.2  0.2
    107       1 /usr/lib/systemd/systemd-re  0.1  0.0
      1       0 /sbin/init                   0.1  0.8
```

**Top processes by CPU:**

```
    PID    PPID CMD                         %MEM %CPU
      1       0 /sbin/init                   0.1  0.8
     52       1 /usr/lib/systemd/systemd-jo  0.2  0.2
    174       1 @dbus-daemon --system --add  0.0  0.1
   1990       1 /usr/lib/polkit-1/polkitd -  0.1  0.1
   1975       1 /usr/libexec/packagekitd     0.2  0.0
```

**Top memory-consuming process:** `/usr/bin/python3 /usr/share...` (PID 212) at 0.2% memory — a Python-based system utility (likely `unattended-upgrades` or similar).

**Observations:**
- Overall resource usage is minimal — all processes below 1% CPU and 0.2% memory.
- `init` (PID 1) leads CPU usage at 0.8%, expected right after boot.
- All top processes are system services; no user workloads running.

---

### 1.3 Service Dependencies

**Dependencies of `multi-user.target`:**

```
multi-user.target
○ ├─apport.service
● ├─console-setup.service
● ├─cron.service
● ├─dbus.service
○ ├─dmesg.service
○ ├─e2scrub_reap.service
○ ├─landscape-client.service
○ ├─networkd-dispatcher.service
● ├─rsyslog.service
```

**Observations:**
- `●` marks active services, `○` marks inactive ones.
- Core services (`cron`, `dbus`, `rsyslog`) are running; optional ones (`landscape-client`, `apport`) are not.
- `dbus.service` is active — required as IPC bus for most system services.

---

### 1.4 User Sessions

**Active sessions:**

```
           system boot  2026-02-26 18:18
           run-level 5  2026-02-26 18:18
LOGIN      tty1         2026-02-26 18:18               211 id=tty1
LOGIN      console      2026-02-26 18:18               206 id=cons
user     - pts/1        2026-02-26 18:18 00:05         350
           pts/2        2026-02-26 18:22              2040 id=ts/2  term=0 exit=0
```

**Login history:**

```
reboot   system boot  6.6.87.2-microso Thu Feb 26 18:18   still running
reboot   system boot  6.6.87.2-microso Thu Feb 26 18:18 - 18:18  (00:00)
reboot   system boot  6.6.87.2-microso Thu Feb 26 18:17 - 18:18  (00:00)

wtmp begins Thu Feb 26 18:17:33 2026
```

**Observations:**
- One active user session on `pts/1`; `pts/2` was a terminated session.
- Kernel version `6.6.87.2-microsoft` confirms WSL2 environment.
- Multiple rapid reboots visible — typical for WSL initialization.

---

### 1.5 Memory Analysis

**Memory overview:**

```
               total        used        free      shared  buff/cache   available
Mem:           7.4Gi       530Mi       6.2Gi       3.5Mi       874Mi       6.9Gi
Swap:          2.0Gi          0B       2.0Gi
```

**Detailed memory info:**

```
MemTotal:        7787724 kB
MemAvailable:    7245304 kB
SwapTotal:       2097152 kB
```

**Observations:**
- ~7.4 GiB total RAM; only 530 MiB used (~7%), system is largely idle.
- 874 MiB in buff/cache — Linux caching filesystem data as expected.
- Swap is allocated (2 GiB) but completely unused — no memory pressure.
- Available memory (6.9 GiB) is higher than free (6.2 GiB) due to reclaimable cache.

---

## Task 2 — Networking Analysis

### 2.1 Network Path Tracing

**Traceroute to github.com:**

```
traceroute to github.com (140.82.121.XXX), 30 hops max, 60 byte packets
 1  WIN-0FR6OLRAJS7.mshome.net (172.30.96.1)  0.611 ms  0.568 ms *
 2  * * *
 3  * * 100.100.1.1 (100.100.1.1)  33.192 ms
 4  100.88.255.254 (100.88.255.254)  33.884 ms  33.843 ms  33.809 ms
 5  10.1.234.1 (10.1.234.1)  33.767 ms  33.741 ms  33.715 ms
 6  ae1-1.rt.irx.vie.at.retn.net (87.245.232.2)  58.161 ms  55.881 ms  55.857 ms
 7  ae11-61.cr3-vie2.ip4.gtt.net (213.39.66.201)  52.996 ms  54.484 ms  54.795 ms
 8  ae33.cr1-fra6.ip4.gtt.net (213.200.114.177)  65.092 ms  65.079 ms  65.067 ms
 9  ip4.gtt.net (87.119.95.178)  60.751 ms  60.727 ms  67.204 ms
10  * * *
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
```

**Observations:**
- 9 visible hops before packets enter GitHub's network (which blocks ICMP).
- Route goes through Vienna (vie) → Frankfurt (fra) via RETN and GTT transit providers.
- Latency jumps from ~34ms (local/ISP) to ~55ms at Vienna, ~65ms at Frankfurt.
- Hops 10–30 show `* * *` — GitHub drops ICMP/traceroute probes at their edge.

**DNS resolution:**

```
;; QUESTION SECTION:
;github.com.                    IN      A

;; ANSWER SECTION:
github.com.             15      IN      A       140.82.121.XXX

;; Query time: 54 msec
;; SERVER: 10.255.255.XXX#53(10.255.255.XXX) (UDP)
```

**Observations:**
- DNS resolved `github.com` to a single A record (`140.82.121.XXX`).
- Low TTL (15s) indicates GitHub uses DNS-based load balancing with frequent rotation.
- DNS server is `10.255.255.XXX` — WSL's internal DNS forwarder.

---

### 2.2 Packet Capture

```
tcpdump: data link type LINUX_SLL2
listening on any, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144 bytes

0 packets captured
0 packets received by filter
0 packets dropped by kernel
```

**Observations:**
- No DNS packets captured during the 10-second window.
- WSL2 uses a virtual network adapter; DNS resolution may go through the Windows host, bypassing the Linux network stack.
- To capture DNS traffic in WSL, one would need to generate DNS queries during the capture window (e.g., run `dig` in parallel).

---

### 2.3 Reverse DNS

**PTR lookup for 8.8.4.4:**

```
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.   3899    IN      PTR     dns.google.

;; Query time: 54 msec
```

**PTR lookup for 1.1.2.2:**

```
;; QUESTION SECTION:
;2.2.1.1.in-addr.arpa.          IN      PTR

;; AUTHORITY SECTION:
1.in-addr.arpa.         1747    IN      SOA     ns.apnic.net. ...

;; Query time: 47 msec
;; status: NXDOMAIN
```

**Comparison:**

| IP       | Status   | PTR Record    | Notes                                      |
|----------|----------|---------------|--------------------------------------------|
| 8.8.4.4  | NOERROR  | dns.google.   | Google's public DNS, PTR properly configured |
| 1.1.2.2  | NXDOMAIN | (none)        | No reverse record exists; SOA from APNIC    |

**Observations:**
- `8.8.4.4` has a valid PTR record (`dns.google.`) — expected for a major public DNS service.
- `1.1.2.2` returns `NXDOMAIN` — unlike `1.1.1.1` (Cloudflare), this IP has no reverse DNS entry configured.
- The SOA in the authority section points to `ns.apnic.net`, meaning APNIC manages the `1.0.0.0/8` reverse zone.