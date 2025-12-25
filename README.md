# homelab-ansible-role-wazuh-agent

Ansible role for installing and configuring the Wazuh agent on Debian/Ubuntu systems.

## Requirements

- Ansible >= 2.15
- Target: Ubuntu (focal, jammy, noble) or Debian (bullseye, bookworm)

## Role Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `wazuh_manager_address` | `wazuh.local.iamrobertyoung.co.uk` | Wazuh manager address |
| `wazuh_manager_port` | `1514` | Wazuh manager port |
| `wazuh_agent_group` | `homelab` | Agent group for centralized configuration |
| `wazuh_agent_name` | `{{ inventory_hostname }}` | Agent name to register with manager |
| `wazuh_registration_password` | `""` | Registration password (if manager requires it) |
| `wazuh_repo_key_url` | `https://packages.wazuh.com/key/GPG-KEY-WAZUH` | Wazuh GPG key URL |
| `wazuh_repo_url` | `https://packages.wazuh.com/4.x/apt/` | Wazuh APT repository URL |

## Usage

### Install via requirements.yml

```yaml
- src: git@github.com:RobertYoung/homelab-ansible-role-wazuh-agent.git
  scm: git
  version: main
  name: wazuh_agent
```

```bash
ansible-galaxy install -r requirements.yml
```

### Example Playbook

```yaml
- hosts: servers
  become: true
  roles:
    - role: wazuh_agent
```

### Override defaults

```yaml
- hosts: servers
  become: true
  roles:
    - role: wazuh_agent
      vars:
        wazuh_manager_address: wazuh.example.com
        wazuh_agent_group: production
```

## What Gets Installed

- Wazuh APT repository and GPG key
- Wazuh agent package
- Agent configuration (`/var/ossec/etc/ossec.conf`)
- Agent service enabled and started

## Supply Chain Security

This project implements [SLSA](https://slsa.dev/) Level 3 provenance for release artifacts.

### Verifying Release Provenance

Download the release artifact and its provenance attestation, then verify:

```bash
# Install slsa-verifier
go install github.com/slsa-framework/slsa-verifier/v2/cli/slsa-verifier@latest

# Download release artifact and provenance from GitHub releases
VERSION="v1.0.0"  # Replace with desired version
curl -LO "https://github.com/RobertYoung/homelab-ansible-role-wazuh-agent/releases/download/${VERSION}/wazuh_agent-${VERSION}.tar.gz"
curl -LO "https://github.com/RobertYoung/homelab-ansible-role-wazuh-agent/releases/download/${VERSION}/wazuh_agent-${VERSION}.tar.gz.intoto.jsonl"

# Verify provenance
slsa-verifier verify-artifact wazuh_agent-${VERSION}.tar.gz \
  --provenance-path wazuh_agent-${VERSION}.tar.gz.intoto.jsonl \
  --source-uri github.com/RobertYoung/homelab-ansible-role-wazuh-agent \
  --source-tag "${VERSION}"
```

## License

MIT
