# Basic Network Scanning with Nmap

## Network Discovery Scan

### Command Used

```bash
sudo nmap -sP 10.0.2.15/24
```

> **Note:** `-sP` (or `-sn` in newer versions of Nmap) performs a host discovery scan without scanning ports.

### Scan Results

```
Starting Nmap 7.98 (https://nmap.org) at 2026-07-15 11:47 -0500

Nmap scan report for 10.0.2.2
Host is up (0.0012s latency).
MAC Address: 52:55:0A:00:02:02 (Unknown)

Nmap scan report for 10.0.2.3
Host is up (0.0012s latency).
MAC Address: 52:55:0A:00:02:03 (Unknown)

Nmap scan report for 10.0.2.15
Host is up.

Nmap done: 256 IP addresses (3 hosts up) scanned in 3.23 seconds
```

### Summary

| IP Address | Status | MAC Address |
|------------|--------|-------------|
| 10.0.2.2 | Up | 52:55:0A:00:02:02 |
| 10.0.2.3 | Up | 52:55:0A:00:02:03 |
| 10.0.2.15 | Up | Local Host |

---

# Port Scan

### Command Used


sudo nmap 10.0.2.15/24
```

### Scan Results

#### Host: 10.0.2.2

```
Host is up (0.0076s latency).

Not shown: 997 filtered TCP ports (no-response)

PORT     STATE  SERVICE
135/tcp  open   msrpc
445/tcp  open   microsoft-ds
7070/tcp open   realserver

MAC Address: 52:55:0A:00:02:02 (Unknown)
```

#### Host: 10.0.2.3

```
Host is up (0.0255s latency).

Not shown: 999 filtered TCP ports (net-unreach)

PORT    STATE SERVICE
53/tcp  open  domain

MAC Address: 52:55:0A:00:02:03 (Unknown)
```

---

# Open Ports Summary

| Host | Open Port | Service | Description |
|------|-----------|----------|-------------|
| 10.0.2.2 | 135/TCP | MSRPC | Microsoft Remote Procedure Call service used for Windows communication. |
| 10.0.2.2 | 445/TCP | Microsoft-DS | SMB service used for file and printer sharing in Windows networks. |
| 10.0.2.2 | 7070/TCP | RealServer | Commonly associated with RealNetworks streaming services or custom applications. |
| 10.0.2.3 | 53/TCP | Domain (DNS) | Domain Name System service used for hostname resolution. |

---

# Observations

- Three hosts were successfully discovered on the `10.0.2.0/24` network.
- Host `10.0.2.2` exposes three TCP services:
  - MSRPC (135)
  - Microsoft-DS (445)
  - RealServer (7070)
- Host `10.0.2.3` is running a DNS service on port 53.
- Most TCP ports on both hosts are filtered, indicating the presence of firewall rules or packet filtering mechanisms.

---

# Conclusion

The Nmap scan successfully identified active hosts within the subnet and detected the services exposed by each system. Such scans are useful during network reconnaissance, asset discovery, and security assessments to identify accessible services and potential attack surfaces.
