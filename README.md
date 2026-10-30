# Arch-Based Audio & DSP Workstations — Configuration History

> Modular documentation for two Linux workstations based on Arch (CachyOS and Garuda Linux).
> The ecosystem is strongly oriented towards: **Audio DSP, Live Coding, Software Development, and Gaming.**
>
> ⚠️ **Privacy & Security**: This documentation is intentionally generic. It contains **no** real usernames, hostnames, passwords, tokens, SSH keys, account IDs, or personal file paths. Standard placeholders (`$USER`, `$HOME`, `~/...`) are used where user-specific values are required.

---

## 🖥️ Machine Profiles

### Computer A — Laptop (CachyOS)

| Component | Details |
|-----------|---------|
| OS | CachyOS Rolling |
| Kernel | CachyOS kernel (7.2.6-1) |
| Session | Wayland |
| Desktop | **COSMIC** (primary) |
| Shell | Fish |
| CPU | AMD Ryzen 7 5700U, 8c / 16t |
| RAM | 12 GiB + 12 GiB swap |
| GPU | AMD Radeon Graphics / Lucienne |
| Audio | AMD Renoir/Cezanne HDMI/DP + Ryzen HD Audio |
| PipeWire/WirePlumber | Active |
| Realtime limits | `ulimit -r = 98`, `ulimit -l = unlimited` |
| Firewall | UFW active |

**Full profile →** [`docs/machine-a-cachyos.md`](docs/machine-a-cachyos.md)

### Computer B — Desktop (Garuda Linux)

| Component | Details |
|-----------|---------|
| OS | Garuda Linux (Arch-based, Zen Kernel) |
| Session | Wayland |
| Shell | Fish |
| CPU | AMD Ryzen (desktop class) |
| RAM | 32 GiB |
| GPU | Radeon iGPU |
| Focus | DAW, Gaming (Lutris), Compilation, Audio Studio |

**Full profile →** [`docs/machine-b-garuda.md`](docs/machine-b-garuda.md)

---

## 📚 Documentation

### 🎛️ Audio & DSP
- [**Audio & DSP Stack**](docs/audio-dsp-stack.md) — PipeWire, JACK, low latency, plugin formats, DAWs
- [**Live Coding & Computer Music**](docs/live-coding-music.md) — SuperCollider, TidalCycles, Sonic Pi, Overtone, Pure Data, CSound
- [**Spatial Audio & Instruments**](docs/spatial-audio-instruments.md) — Ambix, IEM Suite, LinuxSampler, synths

### 💻 Development & System
- [**Dev Toolchain**](docs/dev-toolchain.md) — C/C++, Python, Rust, Go, Lua, JVM, LSP, editors
- [**System Utilities**](docs/system-utilities.md) — Fish, toolbox, desktop apps, package management

### 🎮 Gaming
- [**Gaming & Lutris**](docs/gaming-lutris.md) — Lutris, Wine/Proton, GameMode, MangoHud

---

## 🎯 Configuration Philosophy

```text
Arch-based distro (CachyOS / Garuda)
   +
Fish shell
   +
Wayland (COSMIC and/or Hyprland)
   +
PipeWire + JACK compatibility
   +
Low latency: 48 kHz / quantum 64
   +
Full pro-audio stack (LV2 / LADSPA / VST / VST3 / CLAP / DSSI)
   +
Multi-language dev environment (C/C++, Python, Rust, Go, Lua, JVM, Haskell, Clojure, ...)
   +
Optional Wine plugin bridge (yabridge)
   +
Gaming via Lutris (Wine/Proton)
```

---

## 📝 Documentation Rules

1. **No personal data**: real usernames, hostnames, emails, passwords, tokens, SSH keys, account IDs, or personal paths must **never** be added.
2. **Commands default to Fish** unless explicitly marked otherwise.
3. **Packages** reference official Arch / CachyOS / Garuda repositories or AUR.
4. Use generic placeholders: `$USER`, `$HOME`, `~/...`.

---

## 🚧 Status

### Linux System
- [x] CachyOS (Computer A)
- [x] Garuda Linux (Computer B)
- [x] Fish shell
- [x] COSMIC (Computer A)
- [x] Toolbox & utilities
- [x] C/C++ toolchain
- [x] Python / DSP
- [x] LSP & developer tooling
- [x] Multi-language runtimes
- [x] Editors (Neovim, VS Code, VSCodium)

### Audio
- [x] PipeWire / WirePlumber
- [x] JACK compatibility
- [x] Low-latency configuration
- [x] Full plugin stack (LV2, VST, VST3, CLAP, LADSPA, DSSI)
- [x] DAWs (REAPER, Ardour, Audacity)
- [x] Live coding environments
- [x] Spatial audio stack
- [x] Yabridge (Windows plugin bridge)

### Gaming
- [x] Lutris
- [x] Wine/Proton integration
- [x] GameMode
- [x] MangoHud