# Computer A — CachyOS Laptop

> Hardware and OS-specific profile for the laptop running CachyOS.
> General software stack is documented in the thematic files under `docs/`.

---

## Hardware

| Component | Details |
|-----------|---------|
| CPU | AMD Ryzen 7 5700U, 8 cores / 16 threads |
| RAM | 12 GiB |
| Swap | 12 GiB |
| GPU | AMD Radeon Graphics / Lucienne (integrated) |
| Audio | AMD Renoir/Cezanne HDMI/DP + Ryzen HD Audio |

---

## Operating System

| Component | Details |
|-----------|---------|
| Distribution | CachyOS Rolling |
| Kernel | `linux-cachyos 7.2.6-1` |
| LTS Kernel | `linux-cachyos-lts 6.18.52-1` |
| Session | Wayland |
| Desktop (primary) | **COSMIC** |
| Shell | Fish |

---

## CachyOS-Specific Components

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

---

## System Services & Limits

- **PipeWire / WirePlumber**: active
- **UFW**: active (default incoming: deny, outgoing: allow)
- **Realtime limits**:
  - `ulimit -r = 98`
  - `ulimit -l = unlimited`

---

## Additional Desktop Applications

### Desktop / System
- COSMIC, Alacritty, Kitty
- LightDM, Btrfs Assistant, FSArchiver
- ddcutil, brightnessctl, BlueZ, Flatpak

### Browsers / Communication
- Firefox, Chromium, Element

### Media / Graphics
- VLC components, Celluloid, ImageMagick, Ghostscript

### Development / Assistant
- Claude Desktop, Visual Studio Code, VSCodium

### Package Management
- pacman, yay
- CachyOS Package Installer
- CachyOS Kernel Manager