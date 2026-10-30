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
| AUR helper | **yay** (preferred) |

---

## Garuda-Specific Features

- **Zen Kernel**: optimized for desktop responsiveness and low-latency audio workloads
- **Btrfs + Snapper**: automatic system snapshots with GRUB integration
- **Chaotic-AUR**: pre-built AUR packages enabled by default
- **Garuda Assistant / Garuda Settings**: system optimization GUIs
- **garuda-update**: system update wrapper (handles mirrors, snapshots, AUR)

> ⚠️ `garuda-update` does **not** support a `--mirror` flag.
> Use plain `garuda-update` for updates, and `reflector` for mirror management.

---

## Package Management

### Standard update

```fish
garuda-update
```

### Preferred AUR helper

`yay` is the helper of choice on this machine (instead of `paru`).

```fish
yay -S --needed <package>
```

The `--needed` flag skips packages already installed, which is useful because
Garuda ships many tools out of the box.

### Install a whole package group (Fish syntax)

```fish
yay -S --needed (pacman -Sgq pro-audio)
```

---

## Mirror Management

Some default mirrors can be extremely slow or time out, causing
`failed to retrieve file ... Operation too slow` errors during transactions.

### Install reflector

```fish
yay -S --needed reflector
```

### Automatic ranking (may fail on unstable connections)

```fish
sudo reflector --latest 20 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

### Manual fallback (fast and reliable)

If `reflector` times out on every mirror, force a known-good mirror at the top
of the list:

```fish
# 1. Backup current mirrorlist
sudo cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak

# 2. Put a reliable mirror first
echo "Server = https://mirror.netcologne.de/archlinux/\$repo/os/\$arch" | sudo tee /etc/pacman.d/mirrorlist

# 3. Append the previous list as fallback
cat /etc/pacman.d/mirrorlist.bak | sudo tee -a /etc/pacman.d/mirrorlist > /dev/null
```

---

## Flatpak

Flatpak is used for applications that are painful or unreliable to build from AUR
(notably **Sonic Pi**).

```fish
yay -S --needed flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

Applications installed via Flatpak on this machine:

| Application | Flatpak ID |
|-------------|------------|
| Sonic Pi | `net.sonic_pi.SonicPi` |

---

## Audio Configuration

- **PipeWire / WirePlumber**: active (Garuda default)
- **JACK compatibility**: provided by `pipewire-jack`
- **Realtime privileges**: `realtime-privileges` installed

Add the user to the `realtime` group:

```fish
sudo usermod -aG realtime $USER
```

Verify limits (a logout/login or reboot is required for group changes):

```fish
ulimit -r   # expected: 98
ulimit -l   # expected: unlimited
```

Target latency: **48 kHz / quantum 64** (~1.33 ms).

**Full audio stack →** [`audio-dsp-stack.md`](audio-dsp-stack.md)

---

## Development

- C/C++ toolchain (gcc, clang, cmake, ninja, meson, gdb, lldb)
- Python DSP packages installed **system-wide** via `pacman`/`yay`
- Language servers (clangd, rust-analyzer, gopls, lua-language-server, pylsp, marksman)
- Editors: VSCodium, Neovim
- **GitHub CLI** (`github-cli`) for repository management from the terminal

> Python virtual environments are created **per project**, on demand, using
> `--system-site-packages` to inherit the heavy system packages (NumPy, SciPy, etc.).
> No global "generic" venv is maintained.

**Full toolchain →** [`dev-toolchain.md`](dev-toolchain.md)

---

## Live Coding

Installed on this machine:

- SuperCollider + sc3-plugins
- TidalCycles (`haskell-tidal`)
- FoxDot
- Pure Data
- Csound + csound-plugins
- Faust, ChucK
- Sonic Pi (**via Flatpak**)
- Orca (**terminal version only**, `orca-c-git`)
- Node.js + npm (for Hydra video synth)
- Overtone dependencies (Clojure, Leiningen, JDK 21)

**Full details →** [`live-coding-music.md`](live-coding-music.md)

---

## Gaming

This system uses **Lutris** as the primary gaming platform.

**Full gaming details →** [`gaming-lutris.md`](gaming-lutris.md)

---

## Notes & Gotchas

- **No virtualization**: KVM/libvirt and Windows VMs are **not used** on this
  machine. All Windows gaming is handled through Lutris + Wine/Proton.
- **Hyprland** was originally installed but is not the primary compositor.
- **Double Commander**: the GTK2 variant (`doublecmd-gtk`) no longer exists in
  the repos. Use `doublecmd-qt6`.
- **Orca naming conflict**: the package `orca` in the official repos is the
  GNOME **screen reader**, *not* the Hundred Rabbits live coding language.
  The live coding tool is `orca-c-git` (terminal) or `orca-desktop-git` (GUI, AUR).
- **Orca Desktop GUI**: `orca-desktop-git` currently **fails to build** because
  modern npm blocks the post-install scripts of `electron` / `core-js`, so
  `electron-packager` produces no output. There is **no** `orca-desktop-bin`
  package in AUR. Deferred: install the prebuilt binary from upstream instead.
- **Sonic Pi**: do **not** build from AUR (very long compile, fragile on rolling
  release). Use the Flatpak build.
- **IEM Plugin Suite**: not available as `iem-plugin-suite` in the repos; the
  correct package name must be verified before installation.