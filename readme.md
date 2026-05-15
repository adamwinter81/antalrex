````md
# ANSIBLE REX - Deployment Documentation

## Environment

Ansible control node:

- Hostname: `debian-4gb-nbg1-1`
- OS: Debian GNU/Linux
- Ansible root path: `/ANSIBLE`

Deployment user:

- Local user: `wintera`

Authentication method:

- SSH private key
- Key type: `ED25519`
- Key path:

```bash
/home/wintera/.ssh/antal_rex_ed25519
````

Inventory source:

* Export from Remote Desktop Manager / Devolutions
* Source file: `cv-parser-prod.json`

---

# Directory Structure

```text
/ANSIBLE
├── ansible.cfg
├── inventory
│   └── rex.yml
└── playbooks
```

---

# Installed Components

## Packages

```bash
apt install -y ansible
```

Optional:

```bash
apt install -y tree vim
```

---

# SSH Configuration

## Private Key

Path:

```bash
/home/wintera/.ssh/antal_rex_ed25519
```

Permissions:

```bash
chmod 600 /home/wintera/.ssh/antal_rex_ed25519
```

Key validation:

```bash
ssh-keygen -l -f ~/.ssh/antal_rex_ed25519
```

---

# Ansible Global Configuration

## File

```bash
/ANSIBLE/ansible.cfg
```

## Content

```ini
[defaults]
inventory = /ANSIBLE/inventory/rex.yml
host_key_checking = False
retry_files_enabled = False
timeout = 30

[ssh_connection]
pipelining = True
ssh_args = -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null
```

## Configured Features

* global inventory path
* disabled SSH host key verification
* disabled retry files
* SSH pipelining enabled
* disabled known_hosts persistence
* default timeout set to 30s

---

# Inventory Configuration

## File

```bash
/ANSIBLE/inventory/rex.yml
```

## Inventory Type

* static YAML inventory

## Authentication Variables

```yaml
ansible_connection: ssh
ansible_user: wintera
ansible_port: 22
ansible_python_interpreter: /usr/bin/python3
ansible_ssh_private_key_file: /home/wintera/.ssh/antal_rex_ed25519
```

---

# Managed Hosts

## Reachable Hosts

| Host                 | IP              |
| -------------------- | --------------- |
| cv-parser-prod       | 49.13.137.119   |
| cv-parser-test       | 5.75.241.167    |
| jenkins              | 116.203.118.211 |
| mysql                | 142.132.184.68  |
| n8n                  | 49.13.56.174    |
| php1                 | 49.12.77.5      |
| redis-supervisor-new | 91.99.223.245   |
| rex-lp-wiki          | 49.12.190.164   |
| sentry               | 5.75.229.92     |
| zabbix-gitlab        | 157.90.228.36   |

## Unreachable Hosts

Authentication failure:

| Host       | IP            | Error             |
| ---------- | ------------- | ----------------- |
| dittofeed  | 49.13.22.71   | Permission denied |
| nexus      | 46.224.138.96 | Permission denied |
| nexus-test | 46.224.107.17 | Permission denied |

---

# Verification Commands

## Inventory Validation

```bash
cd /ANSIBLE
ansible-inventory --graph
```

## Connectivity Test

```bash
cd /ANSIBLE
ansible antal_rex -m ping
```

## Single Host Test

```bash
ansible sentry -m ping
```

## Manual SSH Test

```bash
ssh -i ~/.ssh/antal_rex_ed25519 wintera@5.75.229.92
```

---

# Known Issues

## Unreachable Hosts

Following hosts currently reject SSH authentication:

* dittofeed
* nexus
* nexus-test

Current error:

```text
Permission denied (publickey,password)
```

Possible causes:

* missing public key in authorized_keys
* incorrect remote username
* disabled SSH public key authentication
* different SSH key expected

---

# Operational Notes

## Working Directory

Recommended execution path:

```bash
cd /ANSIBLE
```

## Default Inventory

Configured globally in:

```bash
/ANSIBLE/ansible.cfg
```

No `-i` parameter required after configuration.

## SSH Known Hosts

Known hosts verification disabled globally via:

```ini
host_key_checking = False
```

and:

```ini
UserKnownHostsFile=/dev/null
```

---

# Example Operational Commands

## Gather Uptime

```bash
ansible antal_rex -m shell -a "uptime"
```

## Check OS Version

```bash
ansible antal_rex -m shell -a "cat /etc/os-release"
```

## Check Existing User

```bash
ansible antal_rex -m shell -a "id kpala"
```


```
```
