# Live Coding & Computer Music

> SuperCollider, TidalCycles, Sonic Pi, Overtone, Pure Data, CSound, and related environments.

---

## Installed Environments

```text
haskell-tidal
sonic-pi
foxdot
overtone
faust
puredata
supercollider
sc3-plugins
csound
csound-plugins
hydra
orca-c-git
orca-desktop-git
chuck
```

Additional music / composition software:

- Ardour, Audacity, LilyPond, Furnace
- Bespoke Synth, Hydrogen, Guitarix, Freewheeling

---

## SuperCollider

```fish
sudo pacman -S --needed supercollider sc3-plugins
```

Verified version: **SuperCollider 3.14.1**

```fish
sclang -v
scsynth -v
```

---

## Sonic Pi

Verified version: **5.0.0-1**

---

## FoxDot

Verified version: **0.8.12-3**

---

## Overtone

Upstream repository: `Dev/overtone`

Dependencies:

```fish
sudo pacman -S --needed clojure leiningen jdk21-openjdk
sudo archlinux-java set java-21-openjdk
```

Boot verification:

```text
scsynth
PipeWire JACK
48 kHz
block size 64
SuperCollider 3.14.1
Overtone 0.16.3331
```

---

## Orca (Hundred Rabbits)

Both terminal and GUI versions are installed from AUR to cover all workflow preferences:

```fish
yay -S --needed orca-c-git orca-desktop-git
```

- **Terminal version**: Launch with `orca` (ideal for Kitty/Alacritty).
- **Desktop GUI version**: Launch with `orca-desktop` or from the application menu.