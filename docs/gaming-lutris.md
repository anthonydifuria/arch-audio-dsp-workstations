# Gaming — Lutris

> Modern gaming setup based on Lutris, Wine, and Vulkan.
> Replaces the old KVM/libvirt Windows VM configuration previously used on this machine.

---

## Philosophy

This machine uses **Lutris** as the primary gaming platform instead of a Windows virtual machine.

- **No virtualization overhead**: games run natively through translation layers.
- **Proven compatibility**: Lutris provides community-maintained install scripts for thousands of games.
- **Performance**: with Vulkan and GameMode, native-level performance is achievable on most titles.

> ⚠️ **KVM/libvirt and Windows VMs are NOT used on this machine.**
> All Windows gaming is handled through Lutris + Wine/Proton.

---

## Core Installation

### Lutris

```fish
yay -S --needed lutris
```

### Wine (Staging)

`wine-staging` includes additional patches for better game compatibility.

```fish
yay -S --needed wine-staging winetricks
```

### Vulkan (AMD Radeon)

Garuda ships with Vulkan support, but we verify all the necessary drivers are in place:

```fish
yay -S --needed \
  mesa-utils \
  vulkan-radeon lib32-vulkan-radeon \
  lib32-mesa
```

Verify Vulkan is working:

```fish
vulkaninfo | head
```

---

## Performance Optimization

### GameMode

Feral GameMode applies temporary optimizations to the system when a game is running (CPU governor, I/O priority, GPU performance mode).

```fish
yay -S --needed gamemode lib32-gamemode
```

Enable in Lutris:
- Right-click a game → **Configure** → **System options** → **Enable Feral GameMode**.

Or launch any game with:
```fish
gamemoderun ./game-executable
```

### MangoHud

Overlay for monitoring FPS, frametimes, CPU/GPU usage, temperatures, and more.

```fish
yay -S --needed mangohud lib32-mangohud
```

Enable in Lutris:
- Right-click a game → **Configure** → **System options** → **Enable MangoHud**.

Or launch any game with:
```fish
mangohud ./game-executable
```

Combine both:
```fish
mangohud gamemoderun ./game-executable
```

---

## Recommended Wine Prefix Setup

When installing a Windows game through Lutris:

1. **Use the latest Wine-GE or Proton-GE** runner (downloadable directly from Lutris → **Manage Runners**).
2. **Enable DXVK** (DirectX → Vulkan) for DirectX 9/10/11 games.
3. **Enable VKD3D** for DirectX 12 games.
4. **Set Windows version** to Windows 10 in `winecfg`.

---

## Verification Checklist

Before gaming, verify:

- [ ] `lutris` launches without errors.
- [ ] `wine --version` shows a staging version.
- [ ] `vulkaninfo | head` shows the Radeon GPU.
- [ ] `gamemoded --status` shows the daemon is running.
- [ ] `mangohud glxgears` shows the overlay correctly.

---

## Notes & Gotchas

- **Do NOT install KVM/libvirt on this machine**: the gaming setup is fully handled by Lutris. The old VM-based configuration has been deprecated.
- **`wine-staging` vs `wine`**: always prefer `wine-staging` for gaming; it includes many compatibility patches not present in the base `wine` package.
- **32-bit support**: `lib32-*` packages are essential because many Windows games are 32-bit.
- **Proton-GE**: community builds of Valve's Proton with extra patches; often fixes games that stock Proton cannot run.