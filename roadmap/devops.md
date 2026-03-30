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
- **title**: Benchmark Docker I/Operformance
- **description**: Measure Docker I/O performance on the VPS: disk read/write for container writes, network throughput between containers. Use fio for disk, iperf3 for network. Baseline for business tier.
- **inputs**: Docker on OVH VPS, fio, iperf3
- **outputs**: Benchmark report: MB/s read/write, network Gbps; baseline documented
- **dependencies**: [docker_001, ovh_vps_013]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Benchmark script runs and outputs results; performance acceptable for tier

#### Task: docker_018
- **title**: Configure automatic Docker security updates
- **description**: Enable Renovate or Dependabot for Docker base images. Configure docker-compose.yml to watch base images. Create PR workflow when new image versions available.
- **inputs**: Dependabot/Renovate configuration
- **outputs**: Automated PRs for Docker image updates
- **dependencies**: [docker_005]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: PR created when new base image version is available

#### Task: docker_019
- **title**: Document Docker best practices checklist
- **description**: Create a checklist covering all Docker hardening and best practices applied: non-root user in containers, minimal base images, no secrets in environment variables, read-only root filesystem where possible.
- **inputs**: All Docker configuration files
- **outputs**: docs/infrastructure/docker-best-practices.md
- **dependencies**: [docker_001, docker_004, docker_010, docker_011]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Checklist matches actual implementation

---

### Category: Nginx Reverse Proxy Configuration

#### Task: nginx_001
- **title**: Install Nginx
- **description**: Install Nginx via apt. Verify installation. Ensure it's stopped initially (we'll use Docker's nginx or host nginx depending on architecture). Decide: Nginx inside Docker or on host?
- **inputs**: Ubuntu 22.04
- **outputs**: Nginx installed; nginx -v works
- **dependencies**: [docker_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: nginx -v returns version; service nginx status works

#### Task: nginx_002
- **title**: Create Nginx site configuration for Mini-CRM
- **description**: Create /etc/nginx/sites-available/mini-crm with server block: listen 80, server_name customer.domain.com, location / proxy_pass http://localhost:3000 (Nuxt), location /api proxy_pass http://localhost:5432 (PostgreSQL - via unix socket or internal), add security headers.
- **inputs**: Customer domain, Nuxt port
- **outputs**: /etc/nginx/sites-available/mini-crm configured
- **dependencies**: [nginx_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: nginx -t passes; service responds on port 80

#### Task: nginx_003
- **title**: Add security headers to Nginx config
- **description**: Add to Nginx site config: X-Frame-Options SAMEORIGIN, X-Content-Type-Options nosniff, X-XSS-Protection "1; mode=block", Referrer-Policy strict-origin-when-cross-origin, Content-Security-Policy (appropriate for Nuxt PWA).
- **inputs**: Nginx site config
- **outputs**: Security headers present in all responses
- **dependencies**: [nginx_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: curl -I shows all security headers present

#### Task: nginx_004
- **title**: Configure Nginx gzip compression
- **description**: Enable gzip compression in /etc/nginx/nginx.conf: gzip on, gzip_types text/plain text/css application/json application/javascript text/xml application/xml, gzip_min_length 1000.
- **inputs**: /etc/nginx/nginx.conf
- **outputs**: gzip enabled; responses compressed
- **dependencies**: [nginx_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: curl -H "Accept-Encoding: gzip" shows Content-Encoding: gzip in response

#### Task: nginx_005
- **title**: Configure Nginx timeouts and limits
- **description**: Set client_body_timeout 12, client_header_timeout 12, send_timeout 10, keepalive_timeout 15, max_connections 256 to prevent slow-DoS and resource exhaustion.
- **inputs**: /etc/nginx/nginx.conf http block
- **outputs**: Nginx configured with hardened timeout values
- **dependencies**: [nginx_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: nginx -t passes; settings in effect

#### Task: nginx_006
- **title**: Set up Nginx access and error logging
- **description**: Configure access log to /var/log/nginx/mini-crm-access.log combined format. Error log to /var/log/nginx/mini-crm-error.log warn. Set up logrotate for these logs.
- **inputs**: /etc/nginx/nginx.conf
- **outputs**: Logs written; logrotate configured for nginx logs
- **dependencies**: [nginx_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Access log fills after requests; logrotate rotates correctly

#### Task: nginx_007
- **title**: Configure Nginx buffer size limits
- **description**: Set client_body_buffer_size 10K, client_header_buffer_size 1k, large_client_header_buffers 4 8k, proxy_buffer_size 128k, proxy_buffers 4 256k to prevent memory exhaustion from large requests.
- **inputs**: /etc/nginx/nginx.conf http block
- **outputs**: Buffer sizes configured
- **dependencies**: [nginx_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: nginx -t passes; settings applied

#### Task: nginx_008
- **title**: Set up Nginx reverse proxy for Nuxt
- **description**: Configure proxy_pass for Nuxt 3 app: upgrade to websocket support (proxy_set_header Upgrade $http_upgrade), connection (proxy_set_header Connection "upgrade"), host, X-Real-IP, X-Forwarded-For, X-Forwarded-Proto.
- **inputs**: Nginx location blocks
- **outputs**: WebSocket and HTTP proxying working; Nuxt dev tools accessible
- **dependencies**: [nginx_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Nuxt app fully accessible through Nginx with correct headers

#### Task: nginx_009
- **title**: Rate limiting configuration
- **description**: Define two Nginx limit zones: $binary_remote_addr normal (10 req/s) and $binary_remote_addr api (30 req/m). Apply to / and /api endpoints respectively. Return 429 Too Many Requests.
- **inputs**: /etc/nginx/nginx.conf
- **outputs**: Rate limiting active; excessive requests get 429
- **dependencies**: [nginx_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Apache Bench or similar shows 429 after limit exceeded

#### Task: nginx_010
- **title**: Configure Nginx caching for static assets
- **description**: Set up caching for Nuxt static assets: location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ { expires 1y; add_header Cache-Control "public, immutable"; }. For _nuxt hashed files.
- **inputs**: Nginx site config
- **outputs**: Static assets served with 1-year cache; source files get no-cache
- **dependencies**: [nginx_002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: curl -I on static asset shows Cache-Control: public, max-age=31536000

#### Task: nginx_011
- **title**: Set up Nginx redirect HTTP to HTTPS
- **description**: Create separate server block for port 80 that returns 301 to https://$host$request_uri. Only valid for standalone Nginx; for Docker-based, configure nginx container to handle HTTP.
- **inputs**: Nginx site config
- **outputs**: HTTP redirects to HTTPS; HSTS preload prepared
- **dependencies**: [nginx_002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: curl -I http:// redirects with 301 to HTTPS URL

#### Task: nginx_012
- **title**: Configure Nginx worker process settings
- **description**: Set worker_processes auto, worker_rlimit_nofile 65535, worker_connections 4096, use epoll, multi_accept on. Optimizes for OVH VPS specs.
- **inputs**: /etc/nginx/nginx.conf
- **outputs**: Nginx worker configuration optimized
- **dependencies**: [nginx_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: nginx -t passes; worker processes match CPU cores

#### Task: nginx_013
- **title**: Add IP whitelist support for /admin endpoints
- **description**: Create location /admin that only allows access from configured IP whitelist (e.g., customer office IP). Return 403 for all others. Use satisfy any, allow, deny all.
- **inputs**: Customer office IP(s)
- **outputs**: /admin accessible only from whitelist; 403 for others
- **dependencies**: [nginx_002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Request from non-whitelisted IP returns 403 Forbidden

#### Task: nginx_014
- **title**: Configure Nginx upstream keepalive
- **description**: Set up Nginx upstream block with keepalive 32 connections to backend (Nuxt). Reduces upstream TCP handshake overhead for high-traffic scenarios.
- **inputs**: Nginx site config upstream block
- **outputs**: Upstream keepalive configured
- **dependencies**: [nginx_002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: nginx -t passes; keepalive connections visible in nginx stub_status

#### Task: nginx_015
- **title**: Document Nginx configuration runbook
- **description**: Document all Nginx configuration decisions, directives, and their purposes. Include common debugging commands: nginx -t, nginx -s reload, tail -f access.log.
- **inputs**: All Nginx configuration files
- **outputs**: docs/infrastructure/nginx-runbook.md
- **dependencies**: [nginx_001, nginx_002, nginx_003, nginx_009]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Runbook exists and covers all configuration aspects

---

### Category: SSL/TLS Certificates (Let's Encrypt)

#### Task: ssl_001
- **title**: Install Certbot and DNS plugin
- **description**: Install Certbot via snap or apt. Install certbot-nginx plugin. For DNS-01 validation (required for wildcard or behind-VPS scenarios), install certbot-dns-ovh or certbot-dns-cloudflare plugin.
- **inputs**: Ubuntu 22.04, OVH API credentials for DNS
- **outputs**: certbot --version works; dns plugin installed
- **dependencies**: [nginx_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: certbot --version; certbot plugins list shows available plugins

#### Task: ssl_002
- **title**: Obtain Let's Encrypt certificate via HTTP-01
- **description**: Use Certbot with nginx plugin to obtain certificate for customer domain: certbot --nginx -d customer.domain.com. Accept terms, provide email for expiration notices.
- **inputs**: Customer domain pointing to VPS IP, Nginx running
- **outputs**: /etc/letsencrypt/live/customer.domain.com/ with fullchain.pem and privkey.pem
- **dependencies**: [ssl_001, nginx_011]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Certificate obtained; curl https://customer.domain.com works without SSL error

#### Task: ssl_003
- **title**: Configure TLS 1.2 and 1.3 only
- **description**: Edit Nginx SSL configuration: ssl_protocols TLSv1.2 TLSv1.3; remove TLSv1, TLSv1.1. Enable OCSP stapling. Set ssl_prefer_server_ciphers off and use modern cipher suite.
- **inputs**: /etc/nginx/snippets/ssl-params.conf
- **outputs**: TLS 1.2 and 1.3 only; old protocols rejected
- **dependencies**: [ssl_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: SSL Labs test shows grade A, TLS 1.2/1.3 only

#### Task: ssl_004
- **title**: Set up Let's Encrypt auto-renewal
- **description**: Certbot auto-renews via systemd timer (snap install) or cron. Verify: certbot renew --dry-run runs successfully. Ensure renewal hook restarts Nginx.
- **inputs**: Certbot installation
- **outputs**: Auto-renewal timer/cron active; --dry-run passes
- **dependencies**: [ssl_002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: certbot renew --dry-run succeeds; systemctl list-timers shows certbot timer

#### Task: ssl_005
- **title**: Configure OCSP stapling
- **description**: Add to Nginx SSL config: ssl_stapling on, ssl_stapling_verify on, ssl_trusted_certificate /etc/letsencrypt/live/domain.com/chain.pem, resolver 8.8.8.8 8.8.4.4 valid=300s.
- **inputs**: Nginx SSL config
- **outputs**: OCSP stapling enabled; openssl s_client -status shows stapling works
- **dependencies**: [ssl_002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: openssl s_client -connect domain.com:443 -status shows OCSP Response Status: successful

#### Task: ssl_006
- **title**: Generate DH parameters (2048-bit)
- **description**: Generate Diffie-Hellman parameters: openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048. Configure Nginx: ssl_dhparam /etc/ssl/certs/dhparam.pem.
- **inputs**: OpenSSL, Nginx SSL config
- **outputs**: DH parameters generated; Nginx uses them
- **dependencies**: [ssl_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Nginx reloads without error; SSL Labs test shows DH params used

#### Task: ssl_007
- **title**: Set up SSL certificate monitoring
- **description**: Monitor SSL certificate expiration: create script that checks /etc/letsencrypt/renewal/*/webroot_control.py or uses openssl to check expiry. Alert if < 30 days. Integrate with Uptime Kuma or email.
- **inputs**: SSL certificate paths, alert channel
- **outputs**: Alert triggered when cert expires within 30 days
- **dependencies**: [ssl_002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Test by manually checking expiry date; alert fires correctly

#### Task: ssl_008
- **title**: Configure HSTS header
- **description**: Add Strict-Transport-Security header: add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always; to Nginx config. Prepare for HSTS preload submission.
- **inputs**: Nginx site config
- **outputs**: HSTS header present in responses
- **dependencies**: [ssl_003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: curl -I shows HSTS header; SSL Labs test shows HSTS enabled

#### Task: ssl_009
- **title**: Create SSL renewal hook script
- **description**: Create /opt/mini-crm/ssl-renewal-hook.sh that runs on certbot renewal: reloads Nginx, notifies monitoring system, logs to /var/log/ssl-renewal.log.
- **inputs**: Certbot renewal hook
- **outputs**: Hook script exists and is executable; called on renewal
- **dependencies**: [ssl_004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: certbot renew --deploy-hook=/opt/mini-crm/ssl-renewal-hook.sh runs hook

#### Task: ssl_010
- **title**: Document SSL/TLS configuration
- **description**: Document the entire SSL/TLS setup: certificate locations, renewal process, TLS version constraints, cipher suite, OCSP stapling, HSTS, and troubleshooting steps.
- **inputs**: All SSL configuration
- **outputs**: docs/infrastructure/ssl-runbook.md
- **dependencies**: [ssl_001, ssl_002, ssl_003, ssl_004, ssl_005, ssl_008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Document covers all SSL/TLS aspects; matches actual configuration

---

### Category: PostgreSQL Installation & Hardening

#### Task: pg_001
- **title**: Install PostgreSQL 15+ from apt
- **description**: Install PostgreSQL 15 from apt.postgresql.org repository. Install postgresql-15, postgresql-client-15, postgresql-15-postgis-3, postgresql-15-pgqueue (if needed), postgresql-15-pgcrypto.
- **inputs**: Ubuntu 22.04
- **outputs**: PostgreSQL 15 installed; psql --version works; service postgresql running
- **dependencies**: [docker_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: psql --version shows 15+; postgres=# prompt accessible

#### Task: pg_002
- **title**: Configure PostgreSQL data directory
- **description**: For business tier with secondary disk, move PostgreSQL data directory to /data/postgresql. Create directory, chown postgres:postgres, chmod 700. Update postgresql.conf data_directory.
- **inputs**: /data volume, postgresql.conf
- **outputs**: PostgreSQL data on secondary volume; service restarts successfully
- **dependencies**: [pg_001, ovh_vps_013]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: SHOW data_directory; returns /data/postgresql

#### Task: pg_003
- **title**: Create Mini-CRM database and user
- **description**: Create PostgreSQL user minicrm with strong password (generate with pwgen -1 32). Create database minicrm owned by minicrm. Create schema minicrm_schema.
- **inputs**: PostgreSQL superuser access
- **outputs**: Database and user created; minicrm user has no superuser rights
- **dependencies**: [pg_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: \du and \l as superuser show correct roles and ownership

#### Task: pg_004
- **title**: Enable SCRAM-SHA-256 authentication
- **description**: Set password_encryption = scram-sha-256 in postgresql.conf. Rehash passwords for all users. Update pg_hba.conf to use scram-sha-256 for all TCP connections.
- **inputs**: postgresql.conf, pg_hba.conf
- **outputs**: SCRAM-SHA-256 enforced; md5 and trust removed
- **dependencies**: [pg_003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Passwords rehashed as SCRAM; \du shows scram-sha-256 for all users

#### Task: pg_005
- **title**: Configure pg_hba.conf for local and remote access
- **description**: Configure pg_hba.conf: local connections use peer or scram-sha-256 for postgres user, scram-sha-256 for minicrm user. Remote connections: only scram-sha-256 from localhost (via Nginx reverse proxy) or Unix socket. No 0.0.0.0/0.
- **inputs**: pg_hba.conf
- **outputs**: Only local/Unix socket connections allowed; no direct remote access
- **dependencies**: [pg_004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: psql -h /var/run/postgresql from non-postgres user works; direct TCP connection without Nginx fails

#### Task: pg_006
- **title**: Set PostgreSQL listen address to localhost only
- **description**: Set listen_addresses = 'localhost' in postgresql.conf. PostgreSQL only accepts connections from the local machine. All external access goes through Nginx/unix socket.
- **inputs**: postgresql.conf
- **outputs**: PostgreSQL bound to 127.0.0.1; netstat shows only localhost
- **dependencies**: [pg_005]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: psql -h localhost works; psql -h <public_ip> fails

#### Task: pg_007
- **title**: Configure PostgreSQL memory settings
- **description**: Tune postgresql.conf for OVH VPS RAM: shared_buffers = 256MB (starter), 512MB (pro), 1GB (business). Set effective_cache_size, work_mem, maintenance_work_mem appropriately. Set max_connections = 50.
- **inputs**: OVH VPS RAM size, pricing tier
- **outputs**: PostgreSQL memory settings tuned per tier
- **dependencies**: [pg_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: SHOW shared_buffers; matches tier; PostgreSQL restarts without error

#### Task: pg_008
- **title**: Enable PostgreSQL logging
- **description**: Configure postgresql.conf logging: log_destination = 'stderr', logging_collector = on, log_directory = 'log', log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log', log_rotation_age = 1d, log_rotation_size = 100MB. Log: connection log_connections = on, log_disconnections = on, log_duration = off, log_line_prefix = '%m [%p] %q%u@%d '.
- **inputs**: postgresql.conf
- **outputs**: PostgreSQL logs in /var/lib/postgresql/15/main/log/
- **dependencies**: [pg_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Log files appear in log directory; connections/disconnections logged

#### Task: pg_009
- **title**: Enable PostgreSQL slow query logging
- **description**: Set log_min_duration_statement = 1000 (log queries > 1s) in postgresql.conf. This helps identify performance issues. Enable log_lock_waits = on for lock debugging.
- **inputs**: postgresql.conf
- **outputs**: Slow queries and lock waits logged
- **dependencies**: [pg_008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: EXPLAIN ANALYZE query >1s appears in logs

#### Task: pg_010
- **title**: Configure PostgreSQL WAL settings
- **description**: Set wal_level = replica, max_wal_senders = 3, max_replication_slots = 3, wal_keep_size = 1GB. Required for streaming replication and WAL-based backups.
- **inputs**: postgresql.conf
- **outputs**: WAL configured for replication and backup
- **dependencies**: [pg_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: SHOW wal_level; shows replica; pg_is_in_recovery works

#### Task: pg_011
- **title**: Set PostgreSQL max connections per tier
- **description**: Set max_connections: starter=30, pro=50, business=100. Also configure reserved_connections = 3. Monitor with pg_stat_activity.
- **inputs**: postgresql.conf
- **outputs**: Connection limit set per tier
- **dependencies**: [pg_007]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: SHOW max_connections; matches tier

#### Task: pg_012
- **title**: Enable PostgreSQL checkpoint tuning
- **description**: Set checkpoint_completion_target = 0.9, checkpoint_timeout = 15min, max_wal_size = 2GB. Reduces I/O spikes from frequent checkpoints.
- **inputs**: postgresql.conf
- **outputs**: Checkpoint tuning applied
- **dependencies**: [pg_007]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: PostgreSQL restarts successfully; settings applied

#### Task: pg_013
- **title**: Enable PostgreSQL statistics collection
- **description**: Enable pg_stat_statements extension: CREATE EXTENSION pg_stat_statements;. Add shared_preload_libraries = 'pg_stat_statements' in postgresql.conf. Enable track_activities, track_counts, track_io_timing.
- **inputs**: postgresql.conf, SQL superuser access
- **outputs**: pg_stat_statements available; pg_stat_activity shows current queries
- **dependencies**: [pg_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: SELECT * FROM pg_stat_statements LIMIT 1; returns data

#### Task: pg_014
- **title**: Configure PostgreSQL autovacuum
- **description**: Set autovacuum = on, autovacuum_max_workers = 3, autovacuum_naptime = 1min, autovacuum_vacuum_threshold = 50, autovacuum_analyze_threshold = 50, autovacuum_vacuum_scale_factor = 0.1. Critical for table health.
- **inputs**: postgresql.conf
- **outputs**: Autovacuum configured optimally
- **dependencies**: [pg_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: pg_settings shows autovacuum parameters correct

#### Task: pg_015
- **title**: Create PostgreSQL backup role
- **description**: Create role backup_user with nologin, replication, and read-only access to all tables (for pg_dump). Grant USAGE on schemas, SELECT on all tables. Do NOT give write access.
- **inputs**: PostgreSQL SQL
- **outputs**: backup_user role exists with correct permissions
- **dependencies**: [pg_003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: pg_dump -U backup_user -d minicrm works; no write operations succeed

#### Task: pg_016
- **title**: Create PostgreSQL monitoring role
- **description**: Create role pg_monitor with nologin. Grant pg_read_all_settings, pg_read_all_stats, pg_stat_scan_tables. Used by monitoring agents to read stats without superuser.
- **inputs**: PostgreSQL SQL
- **outputs**: pg_monitor role exists; monitoring user can read stats
- **dependencies**: [pg_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: pg_monitor user can query pg_stat_activity without error

#### Task: pg_017
- **title**: Enable PostgreSQL connection pooling hint
- **description**: Document that PgBouncer should be used for connection pooling in front of PostgreSQL. Configure PgBouncer: pool_mode = transaction, max_client_conn = 100, default_pool_size = 20 (starter) / 40 (pro) / 80 (business).
- **inputs**: pgbouncer, postgresql.conf
- **outputs**: PgBouncer installed and configured; Nuxt connects via PgBouncer
- **dependencies**: [pg_001, pg_011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Nuxt app works through PgBouncer; connection limits respected

#### Task: pg_018
- **title**: Set PostgreSQL archive mode
- **description**: Set archive_mode = on, archive_command = '/bin/true' (placeholder for wal-g integration). This enables continuous archiving for point-in-time recovery.
- **inputs**: postgresql.conf
- **outputs**: Archive mode enabled; WAL files archived
- **dependencies**: [pg_010]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: SHOW archive_mode; on; pg_wal files created

#### Task: pg_019
- **title**: Harden PostgreSQL configuration checklist
- **description**: Create a checklist of all PostgreSQL hardening settings: ssl = on, password_encryption = scram-sha-256, listen_addresses, max_connections, shared_buffers, log_connections, log_disconnections, ptrack_enable (if using).
- **inputs**: postgresql.conf
- **outputs**: docs/infrastructure/postgresql-hardening-checklist.md
- **dependencies**: [pg_001, pg_004, pg_006, pg_008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Checklist matches actual configuration

---

### Category: Automated Backup System (BorgBackup/Wal-g)

#### Task: backup_001
- **title**: Evaluate backup tools (BorgBackup vs Wal-g)
- **description**: Compare BorgBackup (deduplicating archiver) vs Wal-g (continuous archiving for PostgreSQL). Choose based on: backup speed, restore speed, deduplication, compression, encrypted transport. Document decision with rationale.
- **inputs**: OVH VPS specs, PostgreSQL size estimates
- **outputs**: Decision document: which tool chosen and why
- **dependencies**: [pg_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Decision documented with comparison matrix

#### Task: backup_002
- **title**: Install BorgBackup
- **description**: Install BorgBackup via apt: apt install borgbackup. Verify installation: borg --version. Create /opt/mini-crm/backup.sh script.
- **inputs**: Ubuntu 22.04
- **outputs**: Borg installed; basic functionality verified
- **dependencies**: [backup_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: borg --version returns version; create/extract/archive works

#### Task: backup_003
- **title**: Create backup repository
- **description**: Initialize Borg repository: borg init --encryption=repokey /var/backups/borg/minicrm. Store encryption key securely in /root/.config/borg/keys/ (or customer's password manager). Set repository permissions to 700.
- **inputs**: Borg installation
- **outputs**: Borg repository initialized; encryption enabled
- **dependencies**: [backup_002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: borg list /var/backups/borg/minicrm succeeds; key stored securely

#### Task: backup_004
- **title**: Write PostgreSQL backup script with Borg
- **description**: Create /opt/mini-crm/backup.sh: (1) pg_dump -Fc minicrm to /tmp, (2) borg create /var/backups/borg/minicrm::{now:%Y-%m-%d_%H-%M} /tmp/dump.sql.gz, (3) borg prune /var/backups/borg/minicrm --keep-daily=7 --keep-weekly=4 --keep-monthly=6, (4) cleanup temp files.
- **inputs**: Borg, PostgreSQL
- **outputs**: backup.sh script executable; manual run succeeds
- **dependencies**: [backup_002, pg_003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Script runs successfully; borg list shows new archive

#### Task: backup_005
- **title**: Add Borg compression to backup script
- **description**: Add --compression lz4 to borg create for faster compression with acceptable ratio. Test backup size with lz4 vs zstd vs none.
- **inputs**: backup.sh
- **outputs**: Compression enabled; backup size reduced
- **dependencies**: [backup_004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: borg list shows compression ratio; backup size measured

#### Task: backup_006
- **title**: Configure automated backup schedule
- **description**: Create systemd timer for daily backups at 2:00 AM Paris time (cron or systemd). Create backup.service (runs backup.sh) and backup.timer (runs daily). Enable and start timer.
- **inputs**: backup.sh
- **outputs**: backup.timer active; backup runs daily
- **dependencies**: [backup_004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: systemctl list-timers shows backup.timer; logs in journalctl

#### Task: backup_007
- **title**: Test backup restore procedure
- **description**: Perform a real restore test: drop a table in minicrm database, run backup script, restore from latest Borg archive using borg extract, pg_restore -Fc, verify table data restored. Document each step.
- **inputs**: Borg backup archive
- **outputs**: Documented restore procedure; table successfully restored
- **dependencies**: [backup_004]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Test table exists after restore; all data intact

#### Task: backup_008
- **title**: Set up remote backup to OVH Object Storage
- **description**: Configure Borg to push backups to OVH Object Storage (Swift-compatible) or an external S3 bucket as off-site backup. Use borg with Rclone or direct S3 backend. This is critical for disaster recovery.
- **inputs**: OVH Object Storage credentials, rclone
- **outputs**: Backups pushed to remote storage; verified accessible
- **dependencies**: [backup_003]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: borg list remote: shows archives; restore from remote succeeds

#### Task: backup_009
- **title**: Create backup verification script
- **description**: Create /opt/mini-crm/verify-backup.sh that: (1) lists recent archives, (2) verifies archive integrity with borg check, (3) extracts a test file to /tmp/verify, (4) cleans up /tmp/verify, (5) sends success/failure notification.
- **inputs**: backup.sh, Borg repository
- **outputs**: verify-backup.sh script; runs post-backup
- **dependencies**: [backup_004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Script runs successfully on healthy backup; detects corruption on corrupted archive

#### Task: backup_010
- **title**: Set backup retention policy
- **description**: Define retention: 7 daily, 4 weekly, 6 monthly, 1 yearly (or based on business need). Configure borg prune command with these parameters. Review with customer for compliance needs.
- **inputs**: Business requirements, legal retention needs
- **outputs**: Retention policy configured; prune runs correctly
- **dependencies**: [backup_004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Old archives pruned according to schedule; space reclaimed

#### Task: backup_011
- **title**: Monitor backup job execution
- **description**: Integrate backup execution monitoring into Uptime Kuma or create systemd service that emails backup logs. Alert on backup failure. Track backup job success/failure history.
- **inputs**: backup.timer, alert channel
- **outputs**: Backup success/failure alerts delivered
- **dependencies**: [backup_006]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **