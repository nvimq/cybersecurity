# Cybersecurity Pentesting Lab

![License](https://img.shields.io/badge/License-MIT-181717?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-Compose-181717?style=flat-square&logo=docker&logoColor=white)

Local environment for security research and vulnerability assessment.

---

## WARNING
**Educational purposes only.** Do not deploy on public networks.

---

<details open>
  <summary><h2>Environment</h2></summary>

<details>
  <summary><h3>Vulnerable Applications & Access</h3></summary>

| Application | Port | Credentials | Description |
|-------------|------|-------------|-------------|
| DVWA | 8080 | `admin:password` | Classic PHP/MySQL vulnerable web app |
| Mutillidae | 8081 | (none required) | OWASP Top 10 vulnerability platform |
| OWASP Juice Shop | 3000 | `user@example.com:changeme` | Modern architecture vulnerabilities |
| Kali Linux | N/A | `root` (internal) | Attacker machine with full toolkit |
| Vulnerable Server | 2222 | `root:toor` | Ubuntu with SSH + Netcat backdoor |
| Netcat Backdoor | 4444 | (no auth) | Direct reverse shell access |

</details>

</details>

---

<details open>
  <summary><h2>Requirements & Installation</h2></summary>

<details open>
  <summary><h3>System Requirements</h3></summary>

| Requirement | Minimum |
|-------------|---------|
| Docker | Latest version |
| Docker Compose | v2.0+ |
| RAM | 4GB+ |
| Disk Space | 10GB+ |
| OS | Linux, macOS, Windows (WSL2) |

</details>

<details open>
  <summary><h3>Quick Installation</h3></summary>

```
git clone https://github.com/nvimq/cybersecurity.git
cd cybersecurity
docker compose up -d
docker compose ps
```

**Access Applications:**
- DVWA: http://localhost:8080
- Mutillidae: http://localhost:8081
- Juice Shop: http://localhost:3000

</details>

</details>

---

<details open>
  <summary><h2>Docker Manual</h2></summary>

<details open>
  <summary><h3>Service Lifecycle</h3></summary>

| Command | Description |
|---------|-------------|
| `docker compose up -d` | Start all services in background |
| `docker compose ps` | List running services and port mappings |
| `docker compose stop` | Stop all containers (data preserved) |
| `docker compose start` | Resume stopped containers |
| `docker compose restart <service>` | Restart specific service |
| `docker compose down` | Stop and remove all containers |
| `docker compose down -v` | FULL CLEANUP (delete volumes) |

</details>

<details open>
  <summary><h3>Logs & Monitoring</h3></summary>

| Command | Description |
|---------|-------------|
| `docker compose logs` | Display logs from all containers |
| `docker compose logs -f` | Stream logs in real-time |
| `docker compose logs -f kali-attacker` | Monitor specific container |
| `docker compose logs --tail 50` | Show last 50 log entries |
| `docker compose logs dvwa` | View DVWA container logs |

</details>

<details open>
  <summary><h3>Building & Updating</h3></summary>

| Command | Description |
|---------|-------------|
| `docker compose build` | Rebuild all images from Dockerfiles |
| `docker compose up -d --build` | Rebuild and start services |
| `docker compose build --no-cache` | Force full rebuild without cache |
| `docker compose build kali-attacker` | Rebuild only Kali container |

</details>

<details open>
  <summary><h3>Kali Container Operations</h3></summary>

| Command | Description |
|---------|-------------|
| `docker compose exec -it kali-attacker bash` | Enter Kali shell (interactive) |
| `docker compose exec kali-attacker whoami` | Execute command without shell |
| `docker compose exec kali-attacker nmap -sV dvwa` | Run nmap from container |
| `docker compose restart kali-attacker` | Restart the Kali container |
| `docker compose pause kali-attacker` | Pause container without stopping |
| `docker compose unpause kali-attacker` | Resume paused container |

</details>

<details open>
  <summary><h3>File Management</h3></summary>

| Command | Description |
|---------|-------------|
| `docker cp <id>:/root/loot/* ./loot/` | Copy files from container to host |
| `docker compose exec kali-attacker ls /root/loot` | List saved results |
| `docker compose exec kali-attacker cp file.txt /root/loot/` | Save file from container |
| `docker system prune` | Clean unused images and containers |
| `docker system df` | Show Docker disk usage |

</details>

</details>

---

<details open>
  <summary><h2>Network Configuration</h2></summary>

<details open>
  <summary><h3>Lab Network Setup</h3></summary>

| Component | Value |
|-----------|-------|
| Network Type | Bridge (`labnet`) |
| Subnet | `172.20.0.0/16` |
| Gateway | `172.20.0.1` |
| DNS | Internal Docker DNS |

</details>

<details open>
  <summary><h3>Container IP Addresses</h3></summary>

| Service | IP Address | Port | Purpose |
|---------|-----------|------|---------|
| kali-attacker | `172.20.0.10` | N/A | Pentesting machine |
| dvwa | `172.20.0.2` | 8080 | Target 1 |
| mutillidae | `172.20.0.3` | 8081 | Target 2 |
| juice-shop | `172.20.0.4` | 3000 | Target 3 |
| vuln-server | `172.20.0.5` | 2222/4444 | Target 4 |

</details>

<details open>
  <summary><h3>Internal Access Examples</h3></summary>

```
# Enter Kali container
docker compose exec -it kali-attacker bash

# Scan all targets by IP
nmap -sV 172.20.0.2 172.20.0.3 172.20.0.4 172.20.0.5

# SQL injection on DVWA
sqlmap -u "http://172.20.0.2/vulnerabilities/sqli/?id=1" --dbs

# SSH to vulnerable server
ssh root@172.20.0.5

# Netcat reverse shell
nc 172.20.0.5 4444

# DNS lookup
dig @172.20.0.1 dvwa
```

</details>

</details>

---

<details open>
  <summary><h2>Installed Tools</h2></summary>

<details open>
  <summary><h3>Network & Reconnaissance</h3></summary>

| Tool | Purpose | Example |
|------|---------|---------|
| `nmap` | Port scanning & service detection | `nmap -sV -p- 172.20.0.2` |
| `dig` | DNS queries | `dig @8.8.8.8 example.com` |
| `nslookup` | DNS lookup | `nslookup example.com 8.8.8.8` |
| `netcat` | Networking utility | `nc -lvnp 4444` |
| `curl` | HTTP requests | `curl -X POST http://dvwa/` |
| `wget` | Download files | `wget http://target/file.txt` |
| `iproute2` | Network configuration | `ip addr show` |
| `net-tools` | Network utilities | `ifconfig` |

</details>

<details open>
  <summary><h3>Web Application Testing</h3></summary>

| Tool | Purpose | Example |
|------|---------|---------|
| `sqlmap` | SQL injection automation | `sqlmap -u "http://dvwa/..." --dbs` |
| `gobuster` | Directory brute-forcing | `gobuster dir -u http://dvwa -w wordlist.txt` |
| `ffuf` | Fast fuzzing | `ffuf -u http://dvwa/FUZZ -w wordlist.txt` |

</details>

</details>

---

<details open>
  <summary><h2>Usage Examples</h2></summary>

<details open>
  <summary><h3>Scenario 1: Basic Network Reconnaissance</h3></summary>

```
# Enter Kali container
docker compose exec -it kali-attacker bash

# Scan all targets in the network
nmap -sV 172.20.0.0/16

# Aggressive scan on DVWA with output
nmap -A 172.20.0.2 -oN /root/loot/dvwa_scan.txt

# Save results as XML
nmap -sV 172.20.0.2 -oX /root/loot/dvwa_scan.xml
```

</details>

<details open>
  <summary><h3>Scenario 2: SQL Injection Testing</h3></summary>

```
# Enter Kali container
docker compose exec -it kali-attacker bash

# Basic SQL injection detection
sqlmap -u "http://dvwa:80/vulnerabilities/sqli/?id=1" --dbs

# SQL injection with authentication
sqlmap -u "http://dvwa/..." --cookie="PHPSESSID=abc123" --dbs

# Dump specific database
sqlmap -u "http://dvwa/..." -D dvwa --dump
```

</details>

<details open>
  <summary><h3>Scenario 3: Directory Enumeration</h3></summary>

```
# Enter Kali container
docker compose exec -it kali-attacker bash

# Gobuster directory scan on Mutillidae
gobuster dir -u http://172.20.0.3 -w /usr/share/wordlists/dirb/common.txt

# FFuzz parameter discovery
ffuf -u http://172.20.0.3/index.php?FUZZ=test -w /usr/share/wordlists/common.txt

# Save results to file
gobuster dir -u http://172.20.0.3 -w wordlist.txt -o /root/loot/gobuster_results.txt
```

</details>

<details open>
  <summary><h3>Scenario 4: SSH Backdoor Access</h3></summary>

```
# Enter Kali container
docker compose exec -it kali-attacker bash

# Direct SSH access
ssh root@172.20.0.5

# SSH with private key
ssh -i /root/.ssh/id_rsa root@172.20.0.5

# Netcat reverse shell
nc 172.20.0.5 4444
```

</details>

<details open>
  <summary><h3>Scenario 5: Saving Results</h3></summary>

```
# Enter Kali container
docker compose exec -it kali-attacker bash

# Run nmap and save results
nmap -sV 172.20.0.2 -oX /root/loot/dvwa_scan.xml
nmap -sV 172.20.0.3 -oN /root/loot/mutillidae_scan.txt

# Run sqlmap and save results
sqlmap -u "http://172.20.0.2/..." --dbs -o /root/loot/sqlmap_results.txt

# List saved files
ls -la /root/loot/

# View on host machine
ls -la ./loot/
```

</details>

</details>

---

<details open>
  <summary><h2>Vulnerability Topics</h2></summary>

<details open>
  <summary><h3>DVWA Training Areas</h3></summary>

| Vulnerability | Category | Difficulty | Attack Vector |
|-------------|----------|-----------|----------------|
| SQL Injection | Injection | Beginner | User input in SQL queries |
| XSS (Stored/Reflected) | Client-Side | Beginner | JavaScript execution in browser |
| CSRF | Authentication | Beginner | Forged requests on behalf of user |
| Command Injection | Injection | Intermediate | OS command execution |
| File Upload | File Handling | Intermediate | Malicious file upload |
| Path Traversal | Directory Traversal | Beginner | Access unauthorized files |
| Brute Force | Weak Auth | Beginner | Guess username/password |

</details>

<details open>
  <summary><h3>Mutillidae Training Areas</h3></summary>

| Vulnerability | Category | Difficulty | Description |
|-------------|----------|-----------|-------------|
| Authentication Bypass | Weak Auth | Beginner | Bypass login mechanisms |
| SQL Injection (Advanced) | Injection | Intermediate | Advanced SQL injection techniques |
| XXE Injection | Injection | Intermediate | XML external entity attacks |
| IDOR | Access Control | Intermediate | Insecure direct object references |
| Sensitive Data Exposure | Data Protection | Beginner | Exposed sensitive information |
| Broken Access Control | Access Control | Intermediate | Privilege escalation |

</details>

<details open>
  <summary><h3>OWASP Juice Shop Training Areas</h3></summary>

| Vulnerability | Category | Difficulty | Attack Type |
|-------------|----------|-----------|------------|
| Injection | Injection | Beginner | SQL, NoSQL injection |
| Broken Authentication | Authentication | Intermediate | Weak password reset |
| Sensitive Data Exposure | Data Protection | Intermediate | Unencrypted data |
| XML External Entities | Injection | Intermediate | XXE attacks |
| Broken Access Control | Access Control | Intermediate | IDOR vulnerabilities |
| Security Misconfiguration | Configuration | Beginner | Default credentials |
| Cross-Site Scripting | Client-Side | Beginner | DOM XSS |

</details>

</details>

---

<details open>
  <summary><h2>Troubleshooting</h2></summary>

<details open>
  <summary><h3>Container Won't Start</h3></summary>

| Problem | Solution |
|---------|----------|
| Container exits immediately | `docker compose logs dvwa` - check error logs |
| Build fails | `docker compose build --no-cache` - rebuild without cache |
| Port already in use | Change port mapping in `docker-compose.yml` |
| Permission denied | Run with `sudo` or add user to docker group |
| Out of memory | Allocate more RAM to Docker Desktop |

**Full Recovery:**
```
docker compose down
docker system prune -a
docker compose up -d --build
```

</details>

<details open>
  <summary><h3>Can't Connect to Applications</h3></summary>

| Problem | Solution |
|---------|----------|
| Port not responding | Verify with `docker compose ps` |
| Network issues | Check with `curl http://172.20.0.2:80` |
| Firewall blocking | Allow ports 8080, 8081, 3000, 2222, 4444 |
| DNS resolution fails | Check `/etc/docker/daemon.json` DNS settings |

**Test Connectivity:**
```
# Linux/Mac
netstat -an | grep 8080

# Windows
netstat -ano | findstr 8080

# Direct container access
docker compose exec -it kali-attacker curl http://dvwa
```

</details>

<details open>
  <summary><h3>Kali Container Exits Immediately</h3></summary>

| Problem | Solution |
|---------|----------|
| Dockerfile issue | `docker compose logs -f kali-attacker` - check logs |
| Missing dependencies | Rebuild: `docker compose up -d --build` |
| Resource constraints | Allocate more CPU/RAM to Docker |

**Debug Kali:**
```
docker compose logs -f kali-attacker
docker compose build --no-cache kali-attacker
docker compose restart kali-attacker
```

</details>

<details open>
  <summary><h3>Insufficient Disk Space</h3></summary>

| Problem | Solution |
|---------|----------|
| Build fails due to space | `docker system prune -a --volumes` |
| Can't pull images | Check disk: `df -h` |
| Containers won't run | Remove old images: `docker images prune -a` |

**Cleanup Commands:**
```
docker system prune -a
docker volume prune
docker image prune -a
```

</details>

<details open>
  <summary><h3>Network Issues Inside Container</h3></summary>

| Problem | Solution |
|---------|----------|
| Can't reach target by IP | Verify IP with `docker inspect <container>` |
| DNS resolution fails | Check network: `docker network inspect labnet` |
| Port forwarding not working | Verify in `docker-compose.yml` port mappings |

**Network Diagnostics:**
```
# From inside Kali
docker compose exec -it kali-attacker bash
ping 172.20.0.2
nslookup dvwa
```

</details>

</details>

---

<details open>
  <summary><h2>Project Information</h2></summary>

<details open>
  <summary><h3>Repository Structure</h3></summary>

```
cybersecurity/
├── docker-compose.yml              # Service orchestration
├── Dockerfile.kali                 # Custom Kali build
├── .github/
│   └── workflows/
│       └── build-and-push.yml      # CI/CD pipeline (GitHub Actions)
├── loot/                           # Shared storage for results
├── README.md                       # Documentation
└── LICENSE                         # MIT License
```

</details>

<details open>
  <summary><h3>File Descriptions</h3></summary>

| File | Purpose |
|------|---------|
| `docker-compose.yml` | Defines all services, networks, volumes, ports |
| `Dockerfile.kali` | Custom build instructions for Kali Linux image |
| `.github/workflows/build-and-push.yml` | GitHub Actions for automatic image building |
| `loot/` | Persistent folder shared with Kali container |
| `README.md` | This documentation file |
| `LICENSE` | MIT License text |

</details>

<details open>
  <summary><h3>Docker Registry (GHCR)</h3></summary>

| Command | Description |
|---------|-------------|
| `docker pull ghcr.io/nvimq/cybersecurity/kali-pentest:latest` | Pull latest image |
| `docker run -it ghcr.io/nvimq/cybersecurity/kali-pentest:latest bash` | Run directly |
| `docker tag <image> ghcr.io/nvimq/cybersecurity/kali-pentest:v1.0` | Tag image |
| `docker push ghcr.io/nvimq/cybersecurity/kali-pentest:v1.0` | Push to registry |

**Available Tags:**
- `latest` - Most recent build
- `<commit-sha>` - Specific commit version
- `v1.0` - Version tags

</details>

<details open>
  <summary><h3>License & Legal</h3></summary>

| Item | Details |
|------|---------|
| License Type | MIT License |
| Copyright | (c) 2025 nvimq |
| Use Case | Educational purposes only |
| Liability | Author not responsible for misuse |
| Commercial Use | Allowed with attribution |

**MIT License Key Points:**
- Free to use and modify
- Must include license notice
- No warranty provided
- No liability accepted

Full text in [LICENSE](LICENSE).

</details>

</details>

