# BigBlueButton Ansible Setup

This repo is a small Ansible playbook for preparing a BigBlueButton server with
Persian/Farsi defaults.

It installs the needed system packages, configures Docker and BigBlueButton,
applies Persian UI and welcome-message settings, installs Greenlight, and creates
an initial Greenlight admin user.

## What is inside

- `playbook.yml` - the main playbook.
- `inventories/hosts.yml` - the target server list.
- `inventories/group_vars/all.yml` - BigBlueButton, domain, locale, SSL, TURN,
  and Greenlight admin settings.
- `roles/` - the install, Docker, prerequisite, Persian config, and admin roles.

## Before running

Make sure the target server has:

- Ubuntu 22.04 for BBB 3.0, or Ubuntu 24.04 for BBB 4.0.
- At least 8 GB RAM and 4 CPU cores.
- A real hostname with DNS already pointing to the server.
- SSH access from your machine.

Then update:

```bash
inventories/hosts.yml
inventories/group_vars/all.yml
```

Keep real passwords, emails, TURN secrets, and host details out of public commits.

## Run

From the repo root:

```bash
ansible-playbook -i inventories/hosts.yml playbook.yml
```

After the playbook finishes, it runs `bbb-conf --check` and prints the BBB URL,
API endpoint, and secret.

## Notes

The default locale is configured as `fa_IR`, and the welcome message is written
for Persian users. TURN is optional in the config, but strongly recommended for a
production server where users may join from restricted networks.
