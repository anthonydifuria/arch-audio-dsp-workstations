# Gaming & Lutris

> Gaming setup using Lutris as the primary platform for running Windows games and applications on Linux.

---

## Lutris

Lutris is the main tool for gaming on both systems. It provides:

- Native Linux game support
- Wine/Proton integration for Windows games
- Emulator management
- Game library organization
- Community install scripts

### Installation

```fish
sudo pacman -S --needed lutris
```

### Additional Gaming Dependencies

```fish
sudo pacman -S --needed \
  wine-staging winetricks \
  lib32-mesa lib32-vulkan-radeon \
  vulkan-radeon mesa-utils \
  gamemode lib32-gamemode \
  mangohud lib32-mangohud
```

### Wine Prefix Management

Lutris handles Wine prefixes automatically, but manual management is available:

```fish
# List Wine prefixes managed by Lutris
ls ~/.local/share/lutris/runners/wine/

# Run Winetricks for a specific prefix
WINEPREFIX=~/.local/share/lutris/runners/winexxx winetricks
```

---

## Gaming Performance Tools

### GameMode

Feral GameMode optimizes system performance on demand:

```fish
# Enable GameMode for a game
gamemoderun ./game-executable

# Or via Lutris (automatic integration)
```

### MangoHud

Performance overlay for monitoring FPS, GPU, CPU, and more:

```fish
# Enable MangoHud
mangohud ./game-executable

# Or via environment variable
MANGOHUD=1 ./game-executable
```

---

## Controller Support

```fish
sudo pacman -S --needed \
  steam-controller \
  xboxdrv \
  ds4drv
```

---

## Notes

- KVM/libvirt and Windows VM are **not used** on this system
- All Windows gaming is handled through Lutris + Wine/Proton
- For specific game configurations, refer to Lutris community scripts