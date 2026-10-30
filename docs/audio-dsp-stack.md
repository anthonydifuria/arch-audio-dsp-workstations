# Audio & DSP Stack

> PipeWire, JACK compatibility, low-latency configuration, plugin formats, and DAWs.

---

## Core Audio Stack

```fish
sudo pacman -S --needed \
  alsa-card-profiles alsa-firmware alsa-lib alsa-plugins \
  alsa-topology-conf alsa-ucm-conf alsa-utils \
  gst-plugin-pipewire libpipewire libsrtp libwireplumber \
  pavucontrol pipewire pipewire-alsa pipewire-audio \
  pipewire-jack pipewire-pulse realtime-privileges \
  vlc-plugin-alsa vlc-plugin-jack wireplumber
```

### Verification

```fish
systemctl --user status pipewire
systemctl --user status wireplumber
wpctl status
pactl info
```

---

## Low Latency Configuration

Target:

```text
Sample rate: 48 kHz
Quantum:     64
```

Applied with:

```fish
pw-metadata -n settings 0 clock.quantum 64
```

At 48 kHz / quantum 64 → **~1.33 ms per buffer**.

Realtime limits:

```text
ulimit -r = 98
ulimit -l = unlimited
```

The `realtime` group must be present for the user.

---

## JACK / Pro Audio Tools

```fish
sudo pacman -S --needed \
  carla qpwgraph jack-example-tools jack_delay jaaa \
  jack_utils a2jmidid mididings
```

### Additional JACK / MIDI Tools

- QjackCtl, jack_mixer, jackmeter, jackminimix, jacktrip
- japa, jconvolver, jack-stdio
- zita-ajbridge, zita-alsa-pcmi, zita-convolver, zita-resampler
- a2jmidid, aconnect, aseqdump
- qmidiarp, qmidictl, qmidinet, qmidiroute, kmidimon, QSynth

**PipeWire JACK** is the preferred compatibility layer.

Virtual MIDI verification:

```fish
aconnect -l
aseqdump -l
```

---

## Plugin Formats

The system supports all major Linux plugin formats:

- **LV2**
- **LADSPA**
- **VST**
- **VST3**
- **CLAP**
- **DSSI**

---

## Plugin Collections

### Core Collections
- Calf, LSP Plugins, x42 Plugins, Zam Plugins
- IEM Plugin Suite, Distrho Ports, DPF Plugins
- Dragonfly Reverb, Zita tools/plugins

### Additional Plugins & Instruments
- ADLPlug, AIDA-X, AMSynth, ArtyFX, Aeolus
- Cardinal, Dexed, DrumGizmo, Drumkv1, Fabla
- Geonkick, GMSynth, Hydrogen, JS80P, Yoshimi
- ZynAddSubFX, padthv1, infamousplugins
- blop, bshapr, bslizr, caps, fomp
- g2reverb, guitarix, freeverb3, EQ10Q
- ebumeter, ecasound, amb-plugins, ambix, jconvolver

### Full Pro-Audio Group (Reference Configuration)

```fish
sudo pacman -S --needed (pacman -Sgq pro-audio)
```

---

## DAWs

- **REAPER** (verified version: 7.79)
- **Ardour**
- **Audacity**

REAPER support dependencies:

```fish
sudo pacman -S --needed lua luarocks liblo portaudio jack-example-tools
```

---

## Windows Plugin Bridge

```text
yabridge
```

Bridges Windows VST / VST3 plugins into the Linux audio stack.