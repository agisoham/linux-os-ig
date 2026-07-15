# linux-nixos

My personal NixOS configuration — Hyprland desktop with a Quickshell-based shell, dynamic Material You theming (matugen), and a triple-boot setup alongside Windows and Ubuntu.

Forked from [ilyamiro/nixos-configuration](https://github.com/ilyamiro/nixos-configuration) and adapted for my own machine. All credit for the original rice, shell, and theming work goes to [ilyamiro](https://github.com/ilyamiro). Desktop previews of the original setup are in [`previews/`](previews/).

> [!NOTE]
> This is a personal config, tuned to my hardware and user account. It is not an installer or a distro — if you want to use it, fork it and audit/adapt it the same way I did.

## Changes from upstream

- Removed passwordless `sudo` (`NOPASSWD`) rule
- Removed the OpenSSH daemon (no remote login service by default)
- Migrated all user references from `ilyamiro` → `AgiSoham` (system user, home-manager, GTK theming paths, shell aliases)
- Switched bootloader from systemd-boot to **GRUB with os-prober** to auto-detect Windows and Ubuntu in a triple-boot setup
- Set Intel CPU microcode updates (upstream is AMD)
- Removed `hardware-configuration.nix` from the repo — it is machine-specific and must be generated locally by the NixOS installer (`.gitignore` keeps it out)

> [!WARNING]
> The upstream README's Arch installer (`curl | bash`) does **not** apply to this repo. Do not run it.

## Install (how I deploy this)

1. Install NixOS normally from the graphical ISO. The installer generates `/etc/nixos/hardware-configuration.nix` for the actual machine — that file stays local and is never committed here.
2. Copy this repo's contents into `/etc/nixos/`, replacing the default `configuration.nix` but **keeping the generated `hardware-configuration.nix`**:

   ```bash
   cd /etc/nixos
   sudo git clone https://github.com/agisoham/linux-nixos.git temp
   sudo cp -r temp/* temp/.gitignore .
   sudo rm -rf temp
   ```

3. Rebuild:

   ```bash
   sudo nixos-rebuild switch
   ```

## Structure

- `configuration.nix` — system-level config (boot, users, services, packages)
- `home.nix` — user environment via home-manager
- `config/` — program configs: Hyprland session, Quickshell widgets, zsh, fonts, and more

## License / attribution

Original work © [ilyamiro](https://github.com/ilyamiro/nixos-configuration); this fork carries my personal modifications on top.
