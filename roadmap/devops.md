# DevOps Roadmap — Mini-CRM

## Objectives

- Provide a fully self-hosted, isolated VPS instance per customer for the Mini-CRM product targeting French artisans
- Ensure enterprise-grade security, reliability, and performance for each tenant on OVH VPS infrastructure
- Enable one-command deployment and automated provisioning to minimize manual onboarding effort
- Establish a sustainable DevOps workflow: build → test → deploy → monitor → backup → recover
- Support tiered pricing (€29/49/79/month) with appropriate resource allocation per tier
- Maintain GDPR-compliant data handling for French artisan businesses

## Subdomains

- **Infrastructure Automation** — Terraform/Pulumi scripts for per-customer VPS provisioning on OVH
- **Container Orchestration** — Docker Compose stacks for Nuxt 3 frontend + PostgreSQL + supporting services
- **Network Security** — Firewall rules, VPN tunnels, SSL/TLS, database connection security
- **Observability** — Monitoring (Uptime Kuma), logging (logrotate + syslog), alerting
- **Backup & Disaster Recovery** — Automated backup schedules with BorgBackup/WAL-g, documented recovery runbooks
- **CI/CD** — GitHub Actions pipelines for build, test, and one-command deployment
- **Cost Governance** — OVH VPS tier selection, resource limits, auto-scaling guardrails

## Milestones

### M1: Foundation — Single Customer Deploy (Week 1–2)
- Manual OVH VPS provisioning, Ubuntu setup, Docker installation, PostgreSQL hardening, SSL, Nginx reverse proxy, basic monitoring, manual backup

### M2: Automation — One-Command Deploy (Week 3–4)
- Bash deployment script wrapping all M1 steps, parameterized for customer
- UFW firewall automation, Let's Encrypt certbot integration, automated backup scheduling

### M3: CI/CD — GitHub Actions Pipeline (Week 5–6)
- GitHub Actions workflow: lint → build → test → push image → deploy to customer VPS via SSH

### M4: Multi-Tenant Hardening (Week 7–8)
- VPN private networking between services, database connection security (scram-sha-256, connection pooling), resource limits per tier

### M5: Observability & DR (Week 9–10)
- Uptime Kuma monitoring, log aggregation, automated backup testing, failover runbook documentation

### M6: Cost Optimization & Scaling (Week 11–12)
- Tier-based resource limits, OVH VPS tier guidance per pricing plan, auto-scaling policies

## Task Categories

---

### Category: OVH VPS Setup (one per customer)

#### Task: ovh_vps_001
- **title**: Create OVH VPS order workflow
- **description**: Design and document the manual or API-driven process for ordering an OVH VPS when a new customer signs up. Include steps for selecting region (France: RBX/SBG/GRA), OS (Ubuntu 22.04 LTS), and add-ons.
- **inputs**: Customer tier (starter/pro/business), desired region
- **outputs**: OVH control panel steps + API script draft for automated order
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Documented runbook or script that results in a running VPS with SSH access

#### Task: ovh_vps_002
- **title**: Generate OVH API credentials
- **description**: Create OVH API credentials (application key, secret, consumer key) for programmatic VPS lifecycle management. Set appropriate ACLs for VPS read/write operations only.
- **inputs**: OVH account credentials
- **outputs**: API key, secret, consumer key stored in secrets manager
- **dependencies**: [ovh_vps_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: API credentials successfully list existing VPS instances via OVH API

#### Task: ovh_vps_003
- **title**: Draft VPS provisioning script
- **description**: Write a bash/python script that uses OVH API to provision a new VPS: select image (Ubuntu 22.04), choose flavor based on pricing tier (starter=Starter-1, pro=Starter-2, business=Starter-4), assign SSH key, configure networking.
- **inputs**: Customer ID, tier, SSH public key, OVH API credentials
- **outputs**: Provisioning script, new VPS IP address and hostname
- **dependencies**: [ovh_vps_002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Script successfully provisions a new VPS and returns SSH connection details

#### Task: ovh_vps_004
- **title**: Map pricing tiers to OVH VPS flavors
- **description**: Document the mapping between Mini-CRM pricing tiers (€29/€49/€79) and OVH VPS model names/specs. Include vCore, RAM, NVMe storage, bandwidth.
- **inputs**: OVH VPS product catalog
- **outputs**: Tier-to-flavor mapping table in docs/infrastructure/pricing-tiers.md
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Mapping table exists and is accurate for all three tiers

#### Task: ovh_vps_005
- **title**: Select OVH data center region per customer
- **description**: Determine optimal OVH data center region for French artisan customers (default: RBX/Roubaix). Create logic to allow region selection based on customer location or preference.
- **inputs**: Customer address/region, available OVH zones
- **outputs**: Selected DC with latency rationale documented
- **dependencies**: [ovh_vps_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Region selection logic documented and implemented in provisioning script

#### Task: ovh_vps_006
- **title**: Configure OVH firewall (Network Firewall)
- **description**: Enable and configure OVH's network-level firewall (firewall DDoS protection) on the VPS public interface. Set default deny, allow SSH (22), HTTP (80), HTTPS (443).
- **inputs**: VPS public IP
- **outputs**: OVH network firewall rules configured
- **dependencies**: [ovh_vps_003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: OVH network firewall UI shows correct rules; test that non-allowed ports are blocked

#### Task: ovh_vps_007
- **title**: Set up OVH reverse DNS (PTR records)
- **description**: Configure reverse DNS (PTR records) for the VPS public IP to resolve to customer-specific hostname (e.g., crm-customerdomain.plesio.fr). Required for email deliverability and SSL validation.
- **inputs**: VPS public IP, desired hostname
- **outputs**: PTR record set via OVH API/UI
- **dependencies**: [ovh_vps_003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: `dig -x <IP>` returns configured hostname

#### Task: ovh_vps_008
- **title**: Bootstrap Ubuntu 22.04 on new VPS
- **description**: After VPS creation, run initial Ubuntu setup: update apt sources, set hostname, configure /etc/hosts, create admin user with sudo, disable root SSH login.
- **inputs**: VPS IP, SSH key, hostname
- **outputs**: Fully bootstrapped Ubuntu 22.04 LTS instance
- **dependencies**: [ovh_vps_003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: SSH connect as admin user, hostname correct, sudo works, root login disabled

#### Task: ovh_vps_009
- **title**: Verify VPS network connectivity
- **description**: Validate VPS networking: ping gateway, ping 8.8.8.8, DNS resolution (dig), NTP sync. Ensure IPv6 is functional.
- **inputs**: VPS IP
- **outputs**: Network diagnostic report
- **dependencies**: [ovh_vps_008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: All network tests pass with expected results

#### Task: ovh_vps_010
- **title**: Document OVH control panel navigation
- **description**: Create a visual/text guide for common OVH VPS management tasks: rebooting, reinstalling OS, viewing stats, managing backups (snapshot), renewing subscription.
- **inputs**: OVH control panel
- **outputs**: docs/infrastructure/ovh-control-panel-guide.md
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Guide covers all common management operations with screenshots/text steps

#### Task: ovh_vps_011
- **title**: Set up OVH VPS monitoring in OVH panel
- **description**: Enable OVH's built-in VPS monitoring: CPU, RAM, disk I/O, network traffic graphs. Configure alert thresholds for disk full, network saturation.
- **inputs**: VPS IP, OVH credentials
- **outputs**: Monitoring dashboard visible in OVH control panel
- **dependencies**: [ovh_vps_003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: OVH panel shows live graphs and alerts are configurable

#### Task: ovh_vps_012
- **title**: Implement VPS lifecycle management script
- **description**: Write a script to manage full VPS lifecycle: provision, reboot, reinstall OS, snapshot, delete. Use OVH API endpoints. Include safety confirmations and idempotency checks.
- **inputs**: Customer ID, action (create/reboot/reinstall/delete), OVH credentials
- **outputs**: Lifecycle management script at scripts/vps-lifecycle.sh
- **dependencies**: [ovh_vps_003]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Script handles all lifecycle actions correctly with proper error handling

#### Task: ovh_vps_013
- **title**: Add secondary disk for data (business tier)
- **description**: For €79/month tier, configure an additional block storage volume (OVH Leslie/Persistent Disk) mounted at /data for PostgreSQL data directory and backups. Include in fstab for reboot persistence.
- **inputs**: VPS IP, OVH API credentials
- **outputs**: /data mounted, persistent across reboots, ~100GB default
- **dependencies**: [ovh_vps_003]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: `lsblk` shows additional volume, `df -h /data` shows capacity

#### Task: ovh_vps_014
- **title**: Create customer VPS inventory sheet
- **description**: Maintain a CSV/Notion DB tracking all customer VPS instances: customer name, domain, VPS IP, OVH service ID, tier, creation date, renewal date, cost.
- **inputs**: Customer onboarding data
- **outputs**: docs/infrastructure/vps-inventory.csv updated on each new customer
- **dependencies**: [ovh_vps_003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Inventory accurate and updated within 24h of new customer onboarding

#### Task: ovh_vps_015
- **title**: Set up OVH scheduled tasks for VPS renewal
- **description**: Configure OVH auto-renew for VPS subscriptions to prevent service interruption. Set renewal 7 days before expiry as a safety buffer.
- **inputs**: OVH service IDs for all active VPS
- **outputs**: Auto-renew configured; calendar reminder set for manual review
- **dependencies**: [ovh_vps_014]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: All VPS show auto-renew enabled in OVH panel

---

### Category: Ubuntu Server Hardening

#### Task: u20_harden_001
- **title**: Disable root SSH login
- **description**: Modify /etc/ssh/sshd_config to set PermitRootLogin no. Restart sshd service. Verify that root cannot SSH in but admin user can.
- **inputs**: /etc/ssh/sshd_config
- **outputs**: Root login disabled; only key-based admin login allowed
- **dependencies**: [ovh_vps_008]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: SSH as root denied; SSH as admin user succeeds

#### Task: u20_harden_002
- **title**: Change default SSH port
- **description**: Change SSH daemon listen port from 22 to a non-standard port (e.g., 2222). Update UFW rules accordingly. Document new port.
- **inputs**: /etc/ssh/sshd_config
- **outputs**: SSH accessible on non-standard port only
- **dependencies**: [u20_harden_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: SSH on port 22 fails; SSH on configured port succeeds

#### Task: u20_harden_003
- **title**: Configure SSH key-only authentication
- **description**: Ensure PasswordAuthentication and ChallengeResponseAuthentication are set to no in sshd_config. Only RSA/ED25519 SSH keys allowed.
- **inputs**: /etc/ssh/sshd_config, customer SSH public key
- **outputs**: Password-based SSH login fully disabled
- **dependencies**: [u20_harden_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: SSH with password fails; SSH with key succeeds

#### Task: u20_harden_004
- **title**: Install and configure Fail2Ban
- **description**: Install Fail2Ban via apt. Configure jail.local to ban IPs after 5 failed SSH attempts for 1 hour. Enable sshd and sshd-ddos jails.
- **inputs**: Fail2Ban package, default config
- **outputs**: Fail2Ban active, /etc/fail2ban/jail.local configured
- **dependencies**: [u20_harden_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Fail2Ban status shows active; test by attempting wrong key and checking ban

#### Task: u20_harden_005
- **title**: Update all system packages
- **description**: Run apt update && apt upgrade -y && apt autoremove -y. Schedule unattended security upgrades via dpkg-reconfigure unattended-upgrades.
- **inputs**: Ubuntu 22.04 fresh install
- **outputs**: All packages updated; unattended-upgrades configured
- **dependencies**: [ovh_vps_008]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: apt list --upgradable shows nothing critical; unattended-upgrades enabled

#### Task: u20_harden_006
- **title**: Configure automatic security updates
- **description**: Install unattended-upgrades package. Configure /etc/apt/apt.conf.d/50unattended-upgrades to automatically apply security updates. Enable邮件 notifications for failed upgrades.
- **inputs**: unattended-upgrades package
- **outputs**: /etc/apt/apt.conf.d/* configured; automatic security updates active
- **dependencies**: [u20_harden_005]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: /var/log/unattended-upgrades/ shows periodic runs; apt shows no pending security updates

#### Task: u20_harden_007
- **title**: Harden /etc/sysctl.conf
- **description**: Apply kernel-level network hardening: disable IP forwarding, disable ICMP redirects, enable TCP SYN cookies, disable source packet routing, disable ICMP broadcast.
- **inputs**: /etc/sysctl.conf
- **outputs**: /etc/sysctl.conf with hardened network settings; sysctl -p executed
- **dependencies**: [ovh_vps_008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: sysctl output matches hardening checklist; kernel parameters applied

#### Task: u20_harden_008
- **title**: Disable unused filesystems
- **description**: Blacklist unused kernel modules to reduce attack surface: cramfs, freevxfs, jffs2, hfs, hfsplus, squashfs, udf, vfat. Add to /etc/modprobe.d/blacklist.conf.
- **inputs**: /etc/modprobe.d/blacklist.conf
- **outputs**: Unused filesystems blacklisted
- **dependencies**: [u20_harden_007]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: lsmod does not show blacklisted modules loaded

#### Task: u20_harden_009
- **title**: Set timezone and configure NTP
- **description**: Set system timezone to Europe/Paris. Install and configure systemd-timesyncd or chrony for NTP. Verify sync with timedatectl.
- **inputs**: OVH VPS fresh install
- **outputs**: Timezone set to Europe/Paris; NTP synchronized
- **dependencies**: [ovh_vps_008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: timedatectl shows NTP synchronized, correct timezone

#### Task: u20_harden_010
- **title**: Createsudo admin user and remove root access
- **description**: Create a non-root admin user with sudo privileges. Add customer's SSH public key to authorized_keys. Document the username for customer.
- **inputs**: Customer SSH public key, desired username
- **outputs**: Admin user created; root shell access disabled
- **dependencies**: [u20_harden_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: New admin user can sudo; root direct login not possible

#### Task: u20_harden_011
- **title**: Harden /etc/passwd, /etc/shadow, /etc/group
- **description**: Ensure only root can write to /etc/passwd and /etc/shadow. Verify group memberships are correct. Remove unnecessary system accounts (games, news, ftp, etc.).
- **inputs**: /etc/passwd, /etc/shadow, /etc/group
- **outputs**: Correct permissions set; unnecessary accounts removed
- **dependencies**: [u20_harden_010]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: ls -la /etc/passwd /etc/shadow /etc/group shows correct permissions

#### Task: u20_harden_012
- **title**: Install and configure AIDE
- **description**: Install AIDE (Advanced Intrusion Detection Environment) for file integrity monitoring. Initialize database, configure daily cron check. Set up alerting on integrity violations.
- **inputs**: AIDE package
- **outputs**: AIDE initialized; cron job running daily; alert on changes
- **dependencies**: [u20_harden_005]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: aide --check runs without errors; test file change triggers alert

#### Task: u20_harden_013
- **title**: Disable IPv6 if not needed
- **description**: If IPv6 is not required for the deployment, disable it to reduce attack surface. Set net.ipv6.conf.all.disable_ipv6=1 and net.ipv6.conf.default.disable_ipv6=1 in sysctl.
- **inputs**: /etc/sysctl.conf
- **outputs**: IPv6 disabled; services still functional
- **dependencies**: [u20_harden_007]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: ip a shows no IPv6 addresses; services still accessible

#### Task: u20_harden_014
- **title**: Set secure umask defaults
- **description**: Set default umask to 027 in /etc/profile, /etc/bash.bashrc, and /etc/login.defs. Ensure new files created by services have appropriate restrictive permissions.
- **inputs**: /etc/profile, /etc/bash.bashrc, /etc/login.defs
- **outputs**: Umask 027 applied system-wide
- **dependencies**: [ovh_vps_008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: New user session shows umask 027; new file permissions are 750/640

#### Task: u20_harden_015
- **title**: Audit running services (remove unnecessary ones)
- **description**: Run systemctl list-units --type=service --state=running to list all running services. Disable and stop unnecessary services (e.g., snap, lxd, avahi-daemon, cups, bluetooth).
- **inputs**: Systemd service list
- **outputs**: Unnecessary services disabled; only essential services running
- **dependencies**: [u20_harden_005]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Only essential services running; unnecessary services masked/disabled

#### Task: u20_harden_016
- **title**: Install and configure libpam-pwquality
- **description**: Install libpam-pwquality for password quality enforcement. Configure /etc/security/pwquality.conf: minlen=14, dcredit=-1, ucredit=-1, lcredit=-1, maxrepeat=2.
- **inputs**: libpam-pwquality package
- **outputs**: Password quality policy enforced for all users
- **dependencies**: [u20_harden_010]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Attempting to set weak password fails with quality check error

#### Task: u20_harden_017
- **title**: Set password expiry policies
- **description**: Configure /etc/login.defs: PASS_MAX_DAYS 90, PASS_MIN_DAYS 7, PASS_WARN_AGE 14. Set similar for existing admin user via chage.
- **inputs**: /etc/login.defs, existing user accounts
- **outputs**: Password expiry policy applied
- **dependencies**: [u20_harden_010]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: chage -l adminuser shows correct expiry settings

#### Task: u20_harden_018
- **title**: Configure auditd for security logging
- **description**: Install auditd. Configure rules to monitor: /etc/passwd modifications, /etc/shadow access, sudo usage, failed authentication attempts, process execution in /usr/bin.
- **inputs**: auditd package
- **outputs**: auditd running; ruleset configured; logs written to /var/log/audit/audit.log
- **dependencies**: [u20_harden_005]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: aureport shows logs; test modification of /etc/passwd appears in audit log

#### Task: u20_harden_019
- **title**: Lock unused user accounts
- **description**: Use passwd -l to lock system accounts that are not needed (daemon, bin, sys, games, man, lp, mail, news, uucp, proxy, www-data, backup, list, irc, gnats).
- **inputs**: /etc/passwd system accounts
- **outputs**: Unused system accounts locked (nologin shell, locked password)
- **dependencies**: [u20_harden_011]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: grep ^${user}: /etc/shadow shows locked accounts have ! in password field

#### Task: u20_harden_020
- **title**: Secure /tmp, /var/tmp, and /dev/shm
- **description**: Mount /tmp with noexec,nosuid,nodev options via /etc/fstab. Similarly secure /var/tmp (bind mount to /tmp). Mount /dev/shm with nosuid,noexec,nodev. These prevent privilege escalation via script execution in temp directories.
- **inputs**: /etc/fstab
- **outputs**: /tmp, /var/tmp, /dev/shm secured with restrictive mount options
- **dependencies**: [u20_harden_007]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: mount | grep tmp and mount | grep shm show correct options

#### Task: u20_harden_021
- **title**: Disable core dumps
- **description**: Disable core dump generation to prevent sensitive data leakage from crashes. Add * hard core 0 to /etc/security/limits.conf and set ulimit -c 0 in systemd services. Disable via sysctl kernel.core_pattern = |/bin/false.
- **inputs**: /etc/security/limits.conf, sysctl settings
- **outputs**: Core dumps disabled system-wide
- **dependencies**: [u20_harden_007]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: ulimit -c returns 0; test program crash does not produce core file

#### Task: u20_harden_022
- **title**: Create hardened SSHD config checklist
- **description**: Create a checklist of all SSHD hardening steps: Protocol 2, Port, PermitRootLogin, PubkeyAuthentication, PasswordAuthentication, ChallengeResponseAuthentication, X11Forwarding no, AllowTcpForwarding no, MaxAuthTries 3, ClientAliveInterval 300, LogLevel VERBOSE.
- **inputs**: /etc/ssh/sshd_config
- **outputs**: docs/infrastructure/sshd-hardening-checklist.md
- **dependencies**: [u20_harden_001, u20_harden_002, u20_harden_003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Each item on checklist verified in current sshd_config

#### Task: u20_harden_023
- **title**: Set up MOTD and login banner
- **description**: Configure /etc/motd and /etc/issue.net with a legal warning banner for unauthorized access notification (French law compliant). This is required for French regulatory compliance.
- **inputs**: Legal text (French), standard MOTD format
- **outputs**: MOTD and SSH login banner configured
- **dependencies**: [ovh_vps_008]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: SSH login shows banner; /etc/motd displays on shell login

---

### Category: Docker & Docker Compose Setup

#### Task: docker_001
- **title**: Install Docker Engine on Ubuntu 22.04
- **description**: Install Docker Engine via official apt repository. Add Docker GPG key, apt source, install docker-ce, docker-ce-cli, containerd.io, docker-compose-plugin. Add admin user to docker group.
- **inputs**: Ubuntu 22.04, admin user
- **outputs**: Docker installed; docker ps works without sudo
- **dependencies**: [u20_harden_005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: docker --version, docker ps, docker-compose --version all succeed

#### Task: docker_002
- **title**: Configure Docker daemon metrics endpoint
- **description**: Enable Docker daemon metrics at tcp://127.0.0.1:9323 for Prometheus scraping. Add metrics-addr = "127.0.0.1:9323" to /etc/docker/daemon.json. Enable experimental features.
- **inputs**: /etc/docker/daemon.json
- **outputs**: curl http://127.0.0.1:9323/metrics returns Docker metrics
- **dependencies**: [docker_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Metrics endpoint responds with Prometheus-format metrics

#### Task: docker_003
- **title**: Configure Docker storage driver
- **description**: Set Docker storage driver to overlay2 (recommended for Ubuntu). Configure log driver to json-file with max-size=10m and max-file=3. Configure default ulimits.
- **inputs**: /etc/docker/daemon.json
- **outputs**: Docker daemon using overlay2, log rotation configured
- **dependencies**: [docker_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: docker info | grep "Storage Driver" shows overlay2; log files limited in size

#### Task: docker_004
- **title**: Secure Docker socket permissions
- **description**: Ensure /var/run/docker.sock has correct permissions (660, owned by root:docker). Verify that only users in docker group can access the socket. Set up docker socket access logging.
- **inputs**: /var/run/docker.sock
- **outputs**: Correct permissions; only docker group members can access
- **dependencies**: [docker_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: ls -la /var/run/docker.sock shows 660 root:docker; non-docker users cannot access

#### Task: docker_005
- **title**: Create docker-compose.yml for Mini-CRM stack
- **description**: Create the main docker-compose.yml defining services: nuxt-frontend (Nuxt 3 PWA), postgresql (PostgreSQL 15+), nginx (reverse proxy), optional: redis (session cache). Use version "3.9" compose format.
- **inputs**: Nuxt 3 app, PostgreSQL version, Redis version
- **outputs**: docker-compose.yml at project root with all services defined
- **dependencies**: [docker_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: docker-compose config validates successfully; all services defined

#### Task: docker_006
- **title**: Create named volumes for persistent data
- **description**: Define named Docker volumes in docker-compose.yml: postgres_data (PostgreSQL data dir), nginx_cache (Nginx cache), app_uploads (customer file uploads). Use local driver with labels.
- **inputs**: docker-compose.yml
- **outputs**: Named volumes created and used by services; docker volume ls shows volumes
- **dependencies**: [docker_005]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: docker volume inspect shows volumes with correct labels; persist after down/up

#### Task: docker_007
- **title**: Configure resource limits per service per tier
- **description**: Add memory and CPU limits to each service in docker-compose.yml based on pricing tier. Starter: 512MB RAM limit; Pro: 1GB; Business: 2GB. Use deploy.resources.limits.
- **inputs**: Tier-to-resource mapping
- **outputs**: docker-compose.yml with tier-specific resource limits
- **dependencies**: [docker_005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: docker stats shows correct limits applied; OOM killer triggers correctly at limit

#### Task: docker_008
- **title**: Set up health checks for all services
- **description**: Add healthcheck directives to each service in docker-compose.yml: nuxt (curl /health), postgresql (pg_isready), nginx (curl localhost:80). Configure restart policy: unless-stopped.
- **inputs**: docker-compose.yml
- **outputs**: All services have healthcheck defined; docker-compose ps shows (healthy)
- **dependencies**: [docker_005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: docker-compose ps shows all services healthy; unhealthy service triggers restart

#### Task: docker_009
- **title**: Configure Docker networks
- **description**: Define two Docker networks: frontend (nginx, nuxt) and backend (nuxt, postgresql, redis). Use bridge driver. Ensure services can only communicate within their network segment.
- **inputs**: docker-compose.yml networks section
- **outputs**: Services segmented; nuxt cannot bypass nginx to reach PostgreSQL directly
- **dependencies**: [docker_005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: docker network inspect shows two networks; services in correct networks

#### Task: docker_010
- **title**: Create Dockerfile for Nuxt 3 frontend
- **description**: Create multi-stage Dockerfile for Nuxt 3: build stage (node:20-alpine, npm ci, npm run build) + production stage (node:20-alpine, copy only .output). Set NODE_ENV=production.
- **inputs**: Nuxt 3 source code
- **outputs**: Dockerfile at project root; docker build succeeds
- **dependencies**: [docker_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Docker image builds and starts successfully; app accessible via nginx

#### Task: docker_011
- **title**: Pin Docker image versions
- **description**: Pin all Docker image versions in docker-compose.yml to specific SHA digests or version tags (not :latest). Document available updates monthly.
- **inputs**: docker-compose.yml
- **outputs**: All images pinned to specific versions; docker-compose pull does not update automatically
- **dependencies**: [docker_005]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: docker-compose.yml has no :latest tags; docker images shows tagged images

#### Task: docker_012
- **title**: Configure Docker logging limits
- **description**: Configure json-file log driver with max-size=10m and max-file=3 for all containers. Set docker-compose.yml default log options. Prevent disk full from log accumulation.
- **inputs**: /etc/docker/daemon.json, docker-compose.yml
- **outputs**: Log files capped at ~30MB per container
- **dependencies**: [docker_003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: du -sh /var/lib/docker/containers/* after 1 week shows bounded log sizes

#### Task: docker_013
- **title**: Create .dockerignore file
- **description**: Create .dockerignore to exclude from build context: node_modules, .git, .nuxt, .output, *.md, tests, .env*, .DS_Store, *.log. Significantly reduces image build time and size.
- **inputs**: Project root files
- **outputs**: .dockerignore file; build context significantly smaller
- **dependencies**: [docker_010]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Build context transfer < 50MB; node_modules not in image

#### Task: docker_014
- **title**: Set up Docker content trust / image signing
- **description**: Enable Docker Content Trust (DOCKER_CONTENT_TRUST=1) environment variable. Ensure images are signed during build. This is critical for supply chain security.
- **inputs**: Docker environment
- **outputs**: DOCKER_CONTENT_TRUST=1 in environment; image signing enforced
- **dependencies**: [docker_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: docker trust key generate succeeds; pulls fail for unsigned images

#### Task: docker_015
- **title**: Create startup script for Docker stack
- **description**: Create scripts/start.sh that performs: docker-compose pull, docker-compose up -d, health check polling (up to 60s), log sample on failure. Create scripts/stop.sh for graceful shutdown.
- **inputs**: docker-compose.yml
- **outputs**: scripts/start.sh and scripts/stop.sh; both executable
- **dependencies**: [docker_005]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: start.sh pulls latest images, starts stack, waits for healthy status

#### Task: docker_016
- **title**: Set up Docker cleanup cron job
- **description**: Create a cron job (weekly) running docker system prune -f --volumes to remove unused containers, networks, images, and volumes. Schedule on Sunday at 3am.
- **inputs**: crontab -e
- **outputs**: Weekly cron job configured; /var/log/docker-cleanup.log written
- **dependencies**: [docker_001]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: cron job runs; docker system df shows reclaimed space after run

#### Task: docker_017
- **title**: Benchmark Docker I/O