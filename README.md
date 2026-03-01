# My Official Desktop Setup

This repository contains Ansible playbooks to automatically provision and configure my CachyOS desktop environment. It is designed for a seamless transition between everyday tasks, high-performance coding, and gaming.

## Features

- **Window Managers:** Hybrid setup with GNOME and a fully configured **Hyprland** (CachyOS optimized).
  - GNOME enhanced with **Multi-Monitor Add-on** (Top bar on all screens).
- **Automation:**
  - Automated **Weekday Startup** (Mon-Fri) for Teams and Slack via a custom bash script.
- **Terminals:** **Ghostty** (native, fast, feature-rich) with Starship prompt.
- **Hardware Drivers:**
  - **NVIDIA:** CachyOS-optimized proprietary drivers for RTX 4060.
  - **Intel:** Media and Vulkan drivers for Arrow Lake iGPU.
  - **Razer:** OpenRazer drivers and Polychromatic for peripheral control.
  - **Webcam:** v4l2loopback for Insta360 and other virtual camera support.
- **Development:** 
  - Node.js & NPM
  - Cursor, Claude Desktop, Slack, Teams
  - GitHub CLI (gh)
  - AI Tools: Gemini CLI, Codex, OpenCode
  - **Docker** & Docker Compose for containerization.
- **Power User CLI:** `eza` (ls), `bat` (cat), `fzf` (fuzzy finder), `ripgrep` (search), `btop` (monitor), `fastfetch` (sysinfo).
- **Gaming:** 
  - **Steam**
  - **MangoHud** for performance overlays.
  - **GameMode** for system optimization.
- **Communication:** Slack (Wayland), Teams, Telegram, and Outlook (Prospect Mail).
- **Networking:** 
  - **Tailscale** for private mesh networking.
  - **NordVPN** with automated split-tunneling (whitelisting Tailscale subnet `100.64.0.0/10`).

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

2. **Run the Playbook:**
   Execute the setup with the following command. You will be prompted for your `sudo` password.
   ```bash
   ansible-playbook -i hosts.ini setup_desktop.yml -K
   ```

## File Structure

- `setup_desktop.yml`: The main playbook containing all installation tasks and service configurations.
- `hosts.ini`: Local inventory file mapping to `localhost`.

## Security Note

The playbook utilizes a temporary `sudoers` rule to allow `paru` to install AUR packages without being blocked by interactive password prompts during the Ansible run. This rule is automatically removed immediately after the AUR tasks complete.
