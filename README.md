# My Official Desktop Setup

This repository contains Ansible playbooks to automatically provision and configure my CachyOS desktop environment. It is designed for a seamless transition between everyday tasks, high-performance coding, and gaming.

## Features

- **Window Managers:** Hybrid setup with GNOME and a fully configured **Hyprland** (CachyOS optimized).
  - GNOME enhanced with **Multi-Monitor Add-on** (Top bar on all screens).
- **Automation:**
  - Automated **Weekday Startup** (Mon-Fri) for Teams and Slack via a custom bash script.
  - Automated **Windows Dynamic Disks (LDM) Mounting** at login for multi-disk stripped volumes.
- **Git Configuration:**
  - **Multi-profile Git** setup using `includeIf`:
    - **Default:** `shawk08033@gmail.com`
    - **Personal (`~/Code/Personal/`):** `shaun@shaunhawk.com`
    - **Work (`~/Code/Huckleberry/`):** `shawk@fsmenergy.com` (Huckleberry projects)
- **Storage:**
  - Automated mounting of **3.6TB Storage** and **3.2TB Games and Programes** Windows volumes to `/mnt/storage` and `/mnt/games`.
- **Network Shares & Discovery:**
  - **NFS & SMB/CIFS** support for connecting to Unraid or other NAS shares.
  - **Avahi (mDNS)** enabled for easy `.local` device discovery.
- **Terminals:** **Ghostty** (native, fast, feature-rich) with Starship prompt.
- **Hardware Drivers:**
  - **NVIDIA:** CachyOS-optimized proprietary drivers for RTX 4060.
  - **Intel:** Media and Vulkan drivers for Arrow Lake iGPU.
  - **Razer:** OpenRazer drivers and Polychromatic for peripheral control.
  - **Webcam:** v4l2loopback for Insta360 and other virtual camera support.
- **Development:** 
  - Node.js, NPM, **Rust**, **Go**, and **Lua**.
  - Cursor, Claude Desktop, **Claude CLI** (`cc-switch`), Slack, Teams.
  - GitHub CLI (gh)
  - AI Tools: Gemini CLI, Codex, OpenCode
  - **Docker** & Docker Compose for containerization.
- **Power User CLI:** `eza` (ls), `bat` (cat), `fzf` (fuzzy finder), `ripgrep` (search), `btop` (monitor), `fastfetch` (sysinfo).
- **Productivity:**
  - **Flameshot** for advanced screenshots and annotations.
- **Gaming:** 
  - **Steam**, **Heroic Games Launcher** (Epic, GOG, Amazon), and **Lutris** (Ubisoft Connect, GOG).
  - **ProtonUp-Qt** for managing Proton/Wine versions.
  - Full **Wine-Staging** environment with 32-bit dependencies for maximum compatibility.
  - **MangoHud** for performance overlays.
- **Communication:** Slack (Wayland), Teams, Telegram, and Outlook (Prospect Mail).
- **Networking:** 
  - **Tailscale** for private mesh networking.
  - **NordVPN** with automated split-tunneling (whitelisting Tailscale subnet `100.64.0.0/10`) and **NordVPN GUI** for desktop management.
- **Security & Hardening:**
  - **UFW Firewall:** Enabled with a "deny" incoming policy.
  - **ClamAV Antivirus:** Daemon and auto-updater (`freshclam`) enabled.
  - **Rkhunter:** Installed and initialized for rootkit detection.
  - **Lynis:** System auditing tool for security hardening.

## Prerequisites

- **OS:** CachyOS (Arch-based)
- **AUR Helper:** `paru`
- **Ansible:** Already installed via the setup process.

## Usage

1. **Clone the repository:**
   ```bash
   git clone <repo-url>
   cd Ansible-Playbooks
   ```

2. **Setup your sensitive variables:**
   - Copy the example file: `cp vars/vault.yml.example vars/vault.yml`
   - Fill in your personal details in `vars/vault.yml`.
   - Create a local `.vault_pass` file with your vault password.
   - Encrypt your vault: `ansible-vault encrypt vars/vault.yml --vault-password-file .vault_pass`

3. **Run the Playbook:**
   Execute the setup with the following command. The vault password will be automatically read from your local `.vault_pass` file (which is ignored by Git).
   ```bash
   ansible-playbook -i hosts.ini setup_desktop.yml -K --vault-password-file .vault_pass
   ```

## File Structure

- `setup_desktop.yml`: The master playbook that includes modular task files.
- `hosts.ini`: Local inventory file mapping to `localhost`.
- `tasks/`: Directory containing modular task files:
  - `system.yml`: System updates and base configuration.
  - `hardware.yml`: Drivers (NVIDIA/Intel), Razer support, and groups.
  - `network.yml`: VPN setup (Tailscale/NordVPN) and split-tunneling.
  - `development.yml`: Dev tools (Node, Docker, Gemini, Codex).
  - `applications.yml`: Official and AUR app installations.
  - `desktop_env.yml`: Hyprland and GNOME extension settings.
  - `cli.yml`: Power user tools and Ghostty terminal.
  - `automation.yml`: Weekday startup script and autostart config.

## Security Note

The playbook utilizes a temporary `sudoers` rule to allow `paru` to install AUR packages without being blocked by interactive password prompts during the Ansible run. This rule is automatically removed immediately after the AUR tasks complete.
