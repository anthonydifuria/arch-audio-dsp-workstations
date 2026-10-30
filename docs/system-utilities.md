# System Utilities

> Toolbox, shell, desktop applications, package management, filesystem tools.

---

## Shell

**Fish** is the primary shell.
CachyOS Fish configuration is installed.
Commands in this documentation are designed for Fish unless explicitly marked otherwise.

---

## Toolbox

```fish
sudo pacman -S --needed \
  base-devel git curl wget unzip zip tar rsync tree file which \
  man-db man-pages less nano neovim htop btop mc zellij tmux \
  fzf ripgrep fd bat eza ncdu jq fastfetch procs dust duf openssh lazygit
```

Additional utilities:

- glances, inxi, 7zip
- btrfs-assistant, btrfs-progs, fsarchiver
- yay, Alacritty, Kitty
- **Double Commander** (file manager)

Main tools:

- Git, Neovim
- htop / btop / glances
- Midnight Commander, Zellij / tmux
- fzf / ripgrep / fd
- bat / eza
- lazygit, OpenSSH
- fastfetch / inxi

---

## Storage / Filesystem Tools

```text
btrfs-progs, btrfs-assistant, fsarchiver
f2fs-tools, exfatprogs, dosfstools
parted, cryptsetup, dmraid, fuse3
```

CachyOS Snapper support is installed.

---

## CachyOS Configuration (Computer A)

```text
cachyos-settings
cachyos-fish-config
cachyos-alacritty-config
cachyos-ananicy-rules
cachyos-kernel-manager
cachyos-packageinstaller
cachyos-hooks
cachyos-snapper-support
cachyos-mirrorlist
cachyos-v3-mirrorlist
cachyos-v4-mirrorlist
cachyos-wallpapers
```