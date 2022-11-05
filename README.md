# home lab

Code for my home lab, managed primarily with Ansible.

## Overview

- This repository is intended to be run using VS Code Devcontainers.
- Ansible playbooks are located in the root folder and are prefixed with two
  numbers, indicating the layer they belong to:
  - `01`: Local Setup
  - `02`: Inventory Provisioning
  - `03`: Node Software Layer
- The organization of the Ansible inventory is `inventory.ini`. `ansible.cfg`
  ensures this file is the default, so it doesn't need to be specified at the
  command line.

## Quick Usage

1. Clone the repository to your workstation.
2. Modify `inventory.ini` and define the servers to manage with Ansible.
3. Run the playbook `01_localhost` to generate local data as a
   prerequisite for managing the inventory.
4. Run any of the playbooks `02_*` to set up the `ansible` user on a freshly
   installed OS with SSH enabled. The following platforms are currently
   supported:
   - Raspberry Pi (`02_rpi.yml`)
5. Run any of the playbooks `03_*` to configure node software to run on the
   OS. The following node software is currently supported:
   - Hashistack (Consul, Vault, Nomad) Server (`03_hashistack_server.yml`)
   - Hashistack (Consul, Vault, Nomad) Client (`03_hashistack_client.yml`)

## Inventory

The playbooks in this repository are designed to work with the following groups:

- `rpi`: Raspberry Pi machines

Below is an empty template to help build `inventory.ini`:

```yaml
[rpi]
server1.example.com
server2.example.com

[rpi:vars]
ansible_user=ansible
ansible_ssh_private_key_file="{{ playbook_dir }}/keys/ansible_ssh_ed25519"
```

## Playbooks

### 01 — Local Setup

#### 01_localhost.yml

This playbook sets up local state on the machine that is required for Ansible to
manage an inventory.

### 02 — Inventory Provisioning

The goal of these playbooks is to take a freshly installed OS and configure it
for further automation with Ansible. This stage ensures the `ansible` user is
properly set up and performs any OS-specific configuration.

#### 02_rpi.yml

This playbook provisions a newly-installed Raspberry Pi by connecting as the
user `pi` and prompting for the current password. It also supports changing the
password for the user `pi`.

### 03 — Node Software Installation

The goal of these playbooks is to install packages and system software necessary
for running applications.

#### 03_hashistack_turnup.yml

This playbook installs HashiCorp Consul, Vault, and Nomad via the OS package
manager and configures the applications to run a cluster.
