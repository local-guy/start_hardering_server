🛠️ Ansible Role: start_server — Basic Server Hardening

This Ansible role performs basic security hardening on a freshly installed Debian/Ubuntu server.
It includes SSH configuration, firewall setup, automatic updates, file integrity monitoring, and other essential security measures.

📁 Project Structure

do_base_hardering.yml      # Main playbook
hosts                      # Inventory file
roles/
  └── start_server/        # Hardening role
       ├── defaults/       # Default variables
       ├── tasks/          # Task definitions
       └── handlers/       # Handlers

✅ What the Role Does
🔐 SSH
- Copies SSH key to server<br>- Disables root login<br>- Disables password authentication<br>- Changes SSH port
🔥 UFW
Enables firewall and allows SSH, HTTP, HTTPS
👤 Users
Creates user
with sudo privileges
🔄 Auto Updates
Configures automatic package updates via
unattended-upgrades
🧱 AIDE
Initializes file integrity checker
📊 Sysctl
Applies kernel-level security settings
🕒 Cron
Sets up daily system integrity checks
Dependencies
------------

⚙️ Default Variables (defaults/main.yml)
remote_user: "bob"
ssh_port: 22
ssh_permit_users: ["{{ remote_user }}"]
local_ssh_key_file: "~/.ssh/id_rsa.pub"

sudo apt update && sudo apt install ansible
ssh-add ~/.ssh/id_rsa
ansible all -i hosts -m ping
ansible-playbook -i hosts do_base_hardering.yml
