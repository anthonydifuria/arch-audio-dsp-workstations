# Spatial Audio & Instruments

> Ambisonics, spatial audio tools, software synthesizers, and samplers.

---

## Spatial Audio Stack

Components present:

- ambix, ambix-lv2
- SSR-related components (where available)
- sound-gambit
- IEM Plugin Suite (standalone + VST3)
- amb-plugins, ambdec
- jconvolver, Zita audio tools

Discovery command (reference configuration):

```fish
pacman -Sgq pro-audio | grep -Ei 'ambi|spat|spatial|surround|hoa|iem|ssr'
```

---

## Synths, Samplers & Instruments

### Installed

- LinuxSampler, QSampler
- SamplV1, Drumkv1, Padthv1
- Yoshimi, ZynAddSubFX, Dexed, JS80P, AMSynth
- Aeolus, FluidSynth, QSynth
- Cardinal, Geonkick, Hydrogen, Bespoke Synth

### Sampler Setup (Reference Configuration)

```fish
sudo pacman -S --needed \
  linuxsampler qsampler samplv1-lv2 samplv1-standalone
```