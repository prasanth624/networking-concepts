## Networking commands
### `ping` – Network Connectivity Check

### Command

```bash
[prasanth@localhost ~]# ping github.com
```

### Output

```
PING github.com (20.207.73.82) 56(84) bytes of data.
64 bytes from 20.207.73.82: icmp_seq=1 ttl=128 time=20.9 ms
64 bytes from 20.207.73.82: icmp_seq=2 ttl=128 time=23.8 ms
^C
--- github.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss
rtt min/avg/max/mdev = 20.934/22.371/23.808/1.437 ms
```

### Explanation

* **0% packet loss** → Network is reachable
* **Low latency (20–23 ms)** → Good network performance
* Used to verify basic connectivity

---

### Limited Ping Count

```bash
[prasanth@localhost ~]# ping github.com -c 2
```

### Output

```
2 packets transmitted, 2 received, 0% packet loss
```

### Use Case

* Script-friendly connectivity checks
* CI/CD pipeline validations

---

### `curl` – HTTP / HTTPS Service Testing

### Command

```bash
[prasanth@localhost ~]# curl -I https://example.com
```

### Output

```
HTTP/2 200
content-type: text/html
server: cloudflare
cf-cache-status: HIT
```

### Explanation

* **HTTP/2 200** → Service is healthy
* Headers confirm:

  * Web server availability
  * CDN / Load Balancer behavior

### DevOps Use Case

* Health checks
* API testing
* Ingress / Load Balancer validation

---

### `ss` – Open Ports & Listening Services

### Command

```bash
[prasanth@localhost ~]# ss -tulnp
```

### Output

```
udp UNCONN 0 0 127.0.0.1:323 users:(("chronyd",pid=929))
tcp LISTEN 0 128 0.0.0.0:22 users:(("sshd",pid=998))
```

### Explanation

* **Port 22 (SSH)** is open and listening
* Shows **process name & PID**
* Replacement for `netstat`

### DevOps Use Case

* Service verification
* Port conflict troubleshooting
* Kubernetes node debugging

---

### `traceroute` – Network Path Analysis

### Command

```bash
[prasanth@localhost ~]# traceroute github.com
```

### Output

```
traceroute to github.com (20.207.73.82), 30 hops max
 1  _gateway (192.168.180.2)  1.299 ms
 2  * * *
 3  * * *
```

### Explanation

* **Hop 1** → Local gateway
* `* * *` → Routers blocking ICMP (common in cloud)
* Identifies routing delays or failures

### DevOps Use Case

* Cloud networking issues
* VPC / subnet routing analysis
* Latency debugging

---

### `nslookup` – DNS Resolution Check

### Command

```bash
[prasanth@localhost ~]# nslookup github.com
```

### Output

```
Server:         192.168.180.2
Address:        192.168.180.2#53

Non-authoritative answer:
Name:   github.com
Address: 20.207.73.82
```

### Explanation

* Confirms DNS resolution
* Shows DNS server in use
* Quick and simple DNS check

---

### `dig` – Detailed DNS Query

### Command

```bash
[prasanth@localhost ~]# dig github.com
```

### Output

```
;; status: NOERROR
;; QUESTION SECTION:
;github.com. IN A

;; ANSWER SECTION:
github.com. 5 IN A 20.207.73.82

;; Query time: 2 msec
;; SERVER: 192.168.180.2#53
;; WHEN: Thu Feb 12 00:18:37 IST 2026
```

### Explanation

* **NOERROR** → DNS query successful
* **TTL = 5 seconds** → CDN-based DNS
* **Query time = 2 ms** → Fast resolution

---

### `telnet` – Basic Port Connectivity Test

### Command

```bash
[prasanth@localhost ~]# telnet github.com 443
```

### Output

```
Trying 20.207.73.82...
Connected to github.com.
Escape character is '^]'.
^CConnection closed by foreign host.
```

### Explanation

* **Connected to github.com** → Port **443 (HTTPS)** is reachable
* Connection succeeds at the **TCP level**
* `^C` → User manually closed the connection
* Telnet does **not** validate TLS; it only confirms port access

### DevOps Use Case

* Validate firewall / security group rules
* Debug service reachability
* Quick port testing in minimal environments

---

### `nc` (Netcat) – Advanced Port Testing

### Command

```bash
[prasanth@localhost ~]# nc -zv github.com 443
```

### Output

```
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Connected to 20.207.73.82:443.
Ncat: 0 bytes sent, 0 bytes received in 0.04 seconds.
```

### Explanation

* **`-z`** → Zero-I/O mode (scan only, no data sent)
* **`-v`** → Verbose output
* Connection successful → Port **443 is open**
* Fast response confirms low network latency



