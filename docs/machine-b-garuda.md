# Computer B — Garuda Linux Desktop

> Hardware and OS-specific profile for the desktop workstation running Garuda Linux.
> General software stack is documented in the thematic files under `docs/`.

---

## Hardware

| Component | Details |
|-----------|---------|
| CPU | AMD Ryzen (desktop class) |
| RAM | 32 GiB |
| GPU | Radeon iGPU |

---

## Operating System

| Component | Details |
|-----------|---------|
| Distribution | Garuda Linux (Arch-based) |
| Kernel | Zen Kernel (Garuda default) |
| Session | Wayland |
| Shell | Fish |

---

## Garuda-Specific Features

- **Zen Kernel**: optimized for desktop responsiveness and low-latency audio workloads
- **Btrfs + Snapper**: automatic system snapshots with GRUB integration
- **Chaotic-AUR**: pre-built AUR packages enabled by default
- **Garuda Assistant / Garuda Settings**: system optimization GUIs
- **garuda-update**: system update wrapper with mirror and snapshot handling

---

## Gaming

This system uses **Lutris** as the primary gaming platform.

**Full gaming details →** [`gaming-lutris.md`](gaming-lutris.md)

---

## Notes

- Hyprland was originally installed on this system but is not actively used as the primary compositor at the moment.
- KVM/libvirt and Windows VM are not used; all Windows gaming is handled through Lutris.