# Audio & DSP Stack

> Professional audio configuration, low-latency setup, DAWs, and plugin collections for Computer B (Garuda Linux).

---

## Core Audio Stack

Garuda Linux uses **PipeWire** and **WirePlumber** by default, which provide excellent low-latency performance and native JACK compatibility.

### Installation

Ensure all core audio components and JACK compatibility layers are installed:

```fish
yay -S --needed \
  alsa-card-profiles alsa-firmware alsa-lib alsa-plugins \
  alsa-topology-conf alsa-ucm-conf alsa-utils \
  gst-plugin-pipewire libpipewire libsrtp libwireplumber \
  pavucontrol pipewire pipewire-alsa pipewire-audio \
  pipewire-jack pipewire-pulse realtime-privileges \
  vlc-plugin-alsa vlc-plugin-jack wireplumber
```

> **Note**: `pipewire-jack` is the critical package that provides the `libjack.so` compatibility layer, allowing JACK-aware applications (like REAPER, SuperCollider, or Carla) to run seamlessly on PipeWire.

---

## Low-Latency & Realtime Configuration

To achieve stable operation at **48 kHz / 64 samples** (~1.33 ms latency) without xruns, the user must have realtime scheduling privileges.

### 1. Add user to the `realtime` group

```fish
sudo usermod -aG realtime $USER
```
*(A logout and login, or a full reboot, is required for this group change to take effect).*

### 2. Verify Realtime Limits

After logging back in, verify that the limits are correctly applied:

```fish
ulimit -r   # Expected: 98 (realtime priority)
ulimit -l   # Expected: unlimited (locked memory)
```

If these values are not correct, Garuda's `realtime-privileges` package may need to be reconfigured in `/etc/security/limits.d/`.

### 3. Restart Audio Services (if needed)

If you make changes to the configuration or group membership, restart the user audio services:

```fish
systemctl --user restart pipewire pipewire-pulse wireplumber
```

---

## Audio Routing & Monitoring Tools

Visual tools to manage connections, monitor levels, and test latency:

```fish
yay -S --needed \
  carla qpwgraph jack-example-tools jack_delay jaaa \
  jack_utils a2jmidid mididings
```

- **Carla**: Plugin host and patchbay.
- **qpwgraph**: Excellent visual patchbay for PipeWire/JACK connections.
- **jack_delay**: The gold standard for measuring round-trip audio latency.
- **jaaa**: JACK Audio Alignment Analyzer (for testing latency and jitter).

---

## Digital Audio Workstations (DAWs)

```fish
yay -S --needed reaper ardour audacity
```

- **REAPER**: Installed via the official Arch package (fully functional evaluation mode, which is effectively unlimited).
- **Ardour**: Open-source professional DAW.
- **Audacity**: Quick audio editing and waveform manipulation.

---

## Plugin Collections

### Core Mixing & Mastering Plugins

```fish
yay -S --needed \
  calf lsp-plugins x42-plugins zam-plugins \
  distrho-ports dpf-plugins \
  dragonfly-reverb zita-convolver zita-resampler
```

### Comprehensive Pro-Audio Group

Arch Linux provides a `pro-audio` package group containing dozens of synthesizers, samplers, and effects. Install the entire group to have every official option available:

```fish
yay -S --needed (pacman -Sgq pro-audio)
```

*(This includes Yoshimi, Dexed, AMSynth, LinuxSampler, Drumkv1, and many more).*

> ⚠️ **Gotcha**: The package `iem-plugin-suite` is **not** available under that exact name in the official repos. Verify the correct package name (e.g., via `pacman -Ss iem`) before attempting installation.

---

## Verification Checklist

Before starting a low-latency session, verify:

1. [ ] User is in the `realtime` group (`groups $USER`).
2. [ ] `ulimit -r` returns `98` and `ulimit -l` returns `unlimited`.
3. [ ] PipeWire and WirePlumber are running (`systemctl --user status pipewire wireplumber`).
4. [ ] Applications recognize JACK via PipeWire (e.g., Carla or REAPER shows "JACK" as an available backend).
5. [ ] Target sample rate is set to **48000 Hz** and buffer size to **64** in the DAW or `qpwgraph`/`helvum`.

---

## Notes & Gotchas

- **Do not install `jack2`**: On modern Garuda/Arch, `pipewire-jack` completely replaces the standalone `jack2` daemon. Installing both can cause conflicts.
- **PulseAudio emulation**: `pipewire-pulse` handles all legacy PulseAudio applications (like web browsers or Discord) seamlessly.
- **ALSA applications**: `pipewire-alsa` provides the `alsa-plugins` hook to route pure ALSA apps through PipeWire.