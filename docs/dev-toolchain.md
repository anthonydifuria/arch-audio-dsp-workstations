# Development Toolchain

> Core compilers, build systems, language servers, and editor configurations for Computer B (Garuda Linux).

---

## Core Build Tools (C/C++ & General)

Essential tools for compiling software, building plugins, and general development.

```fish
yay -S --needed \
  gcc clang llvm cmake ninja gdb lldb make meson ccache pkgconf \
  autoconf automake libtool binutils bison flex
```

---

## Python Environment Strategy

> ⚠️ **Do NOT create a global "generic" virtual environment.**
> Heavy data-science and DSP packages are installed **system-wide** via the package manager. This avoids recompiling massive C-extensions (like NumPy/SciPy) and ensures optimal performance.

### 1. System-wide DSP Packages

```fish
yay -S --needed \
  python-numpy python-scipy python-matplotlib python-pandas \
  python-numba python-sympy python-soundfile python-librosa \
  python-pyaudio python-mido python-pyqt6
```

### 2. Per-Project Virtual Environments

When starting a new project, create a venv **inside the project directory** that inherits the system packages:

```fish
# Navigate to your project
cd ~/Dev/my-audio-project

# Create venv inheriting system site-packages
python -m venv --system-site-packages .venv

# Activate (Fish shell)
source .venv/bin/activate.fish

# Install lightweight, project-specific dependencies via pip
pip install sounddevice jupyterlab python-osc
```

---

## Language Server Protocol (LSP)

Provides autocompletion, go-to-definition, and inline diagnostics for Neovim and VSCodium.

```fish
yay -S --needed \
  clang-tools-extra \
  rust-analyzer \
  gopls \
  lua-language-server \
  python-lsp-server \
  marksman
```

---

## Editors

### VSCodium

The open-source, telemetry-free build of VS Code. Installed via AUR binary to avoid compilation.

```fish
yay -S --needed vscodium-bin
```

Launch with:
```fish
codium
```

### Neovim

For terminal-based editing (configured separately in `~/.config/nvim`).

```fish
yay -S --needed neovim
```

---

## Version Control & Repository Management

### Git

Standard version control (usually pre-installed on Garuda, but verified here).

```fish
yay -S --needed git
```

### GitHub CLI (`gh`)

Official GitHub command-line tool for managing repositories, issues, PRs, and GitHub Actions directly from the terminal.

```fish
yay -S --needed github-cli
```

#### Initial Setup

Authenticate with GitHub (follow the interactive prompts):

```fish
gh auth login
```

Verify authentication:

```fish
gh auth status
```

#### Common Workflows

- Clone a repo: `gh repo clone owner/repo`
- Create a PR: `gh pr create`
- View CI runs: `gh run watch`
- List issues: `gh issue list`

---

## Notes & Gotchas

- **Python `--system-site-packages`**: This is the key to a fast, clean Python workflow on Arch. You get the speed of pre-compiled Arch packages without polluting the global Python environment with project-specific junk.
- **VSCodium vs VS Code**: `vscodium-bin` is used to avoid Microsoft telemetry and licensing restrictions, while maintaining 100% extension compatibility via the Open VSX Registry.
- **LSP Servers**: Ensure your editor is configured to point to these executables (e.g., `clangd` for C/C++, `pylsp` for Python). Garuda/Arch keep these perfectly up-to-date.