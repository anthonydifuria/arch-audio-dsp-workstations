# Live Coding & Computer Music

> SuperCollider, TidalCycles, Sonic Pi, Overtone, Pure Data, CSound, and related environments.

---

## Installed Environments

```text
haskell-tidal
sonic-pi (Flatpak)
foxdot
overtone (dependencies installed)
faust
puredata
supercollider
sc3-plugins
csound
csound-plugins
hydra (Node.js)
orca-c-git
chuck
```

Additional music / composition software:

- Ardour, Audacity, LilyPond, Furnace
- Bespoke Synth, Hydrogen, Guitarix, Freewheeling

---

## SuperCollider

```fish
yay -S --needed supercollider sc3-plugins
```

Verified version: **SuperCollider 3.14.1**

```fish
sclang -v
scsynth -v
```

---

## Sonic Pi

> ⚠️ **Do NOT install from AUR.** The AUR package `sonic-pi` compiles from source
> and takes a very long time, often failing on rolling release distros.
> Use **Flatpak** instead (official recommendation for Linux).

### Installation via Flatpak

```fish
yay -S --needed flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install flathub net.sonic_pi.SonicPi
```

### Launch

```fish
flatpak run net.sonic_pi.SonicPi
```

Or find it in the application menu.

---

## FoxDot

```fish
yay -S --needed foxdot
```

Verified version: **0.8.12-3**

FoxDot requires SuperCollider and uses it as the audio backend.

---

## TidalCycles

```fish
yay -S --needed haskell-tidal
```

TidalCycles is a live coding environment for musical patterns, written in Haskell.
It requires SuperCollider with SuperDirt quark for audio output.

---

## Overtone

Overtone is a Clojure-based live coding environment. Install the dependencies:

```fish
yay -S --needed clojure leiningen jdk21-openjdk
sudo archlinux-java set java-21-openjdk
```

After installation, verify Java version:

```fish
java -version
```

Expected: **openjdk version "21.x.x"**

Boot verification (in a Clojure REPL with Overtone):

```text
scsynth
PipeWire JACK
48 kHz
block size 64
SuperCollider 3.14.1
Overtone 0.16.3331
```

---

## Pure Data

```fish
yay -S --needed puredata
```

Pure Data (Pd) is a visual programming language for music and multimedia.

---

## Csound

```fish
yay -S --needed csound csound-plugins
```

Csound is a sound and music computing system.

---

## Faust

```fish
yay -S --needed faust
```

Faust is a functional programming language for real-time signal processing and synthesis.

---

## ChucK

```fish
yay -S --needed chuck
```

ChucK is a strongly-typed, strongly-timed, concurrent, on-the-fly audio programming language.

---

## Orca (Hundred Rabbits)

> ⚠️ **Naming conflict**: the package `orca` in the official Arch repos is the
> GNOME **screen reader** for visually impaired users, NOT the Hundred Rabbits
> live coding tool.

### Terminal Version (Recommended)

```fish
yay -S --needed orca-c-git
```

Launch with:

```fish
orca
```

Ideal for use with Kitty, Alacritty, or other terminals.

### Desktop GUI Version (Deferred)

The AUR package `orca-desktop-git` currently **fails to build** because modern
npm blocks the post-install scripts of `electron` and `core-js`, causing
`electron-packager` to produce no output.

There is **no** `orca-desktop-bin` package in AUR.

**Workaround**: download the prebuilt binary directly from:
```
https://hundredrabbits.itch.io/orca
```

Extract and place in `~/Applications/Orca` or similar.

---

## Hydra (Video Synth)

Hydra is a live coding video synth. It can be used directly in the browser at:
```
https://hydra.ojack.xyz/
```

For local/offline use, install Node.js and npm:

```fish
yay -S --needed nodejs npm
```

Then clone the Hydra repository and run locally:

```fish
git clone https://github.com/hydra-synth/hydra
cd hydra
npm install
npm start
```

---

## Additional Tools

### GitHub CLI

For managing repositories, issues, and PRs from the terminal:

```fish
yay -S --needed github-cli
```

Authenticate with:

```fish
gh auth login
```

---

## Audio Backend

All live coding environments should be configured to use:

- **PipeWire** with JACK compatibility (`pipewire-jack`)
- **Sample rate**: 48 kHz
- **Buffer size**: 64 samples (for ~1.33 ms latency)
- **Realtime privileges**: user must be in the `realtime` group

See [`audio-dsp-stack.md`](audio-dsp-stack.md) for full audio configuration.

---

## Notes & Gotchas

- **Sonic Pi**: always use Flatpak, never compile from AUR
- **Orca**: terminal version (`orca-c-git`) works perfectly; desktop version
  requires manual binary download due to npm build issues
- **Overtone**: requires Java 21 and Clojure; set as default with `archlinux-java`
- **Hydra**: browser-based is easiest; local install requires Node.js
- **All environments**: must be configured for PipeWire/JACK at 48kHz/64 samples