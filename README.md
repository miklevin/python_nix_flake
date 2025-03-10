# Python Nix Flake with UV Venv

[![Nix Flake](https://img.shields.io/badge/Nix-Flake-blue.svg)](https://nixos.org) [![Python 3.13](https://img.shields.io/badge/Python-3.13-green.svg)](https://www.python.org) [![UV](https://img.shields.io/badge/UV-Enabled-orange.svg)](https://github.com/astral-sh/uv)

A modern, reproducible Python development environment using Nix Flakes and `uv` for fast dependency management and virtual environments. This flake replaces traditional `pip` and `virtualenv` with `uv`, streamlining setup across Linux, macOS, and Windows (via WSL), with optional CUDA support. Perfect for AI projects, data science, or any Python workflow needing JupyterLab and beyond.

## Features

- **Cross-Platform**: Works on Linux, macOS, and Windows (WSL) with a single `flake.nix`.
- **Fast Setup**: Uses `uv` for quicker virtual environment creation and dependency installation.
- **Reproducible**: Nix ensures consistent environments across machines.
- **JupyterLab Ready**: Launch JupyterLab with `start` and stop it with `stop`.
- **CUDA Support**: Auto-detects and configures CUDA on Linux if available.
- **Customizable**: Add your Python dependencies in `requirements.txt`.

## Prerequisites

- [Nix](https://nixos.org/download.html) installed with Flake support enabled.
- A `requirements.txt` file (optional, see example below).

## Quick Start

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/miklevin/python_nix_flake.git
   cd python_nix_flake
   ```

2. **Enter the Development Shell**:
   ```bash
   nix develop
   ```
   This sets up the virtual environment with `uv` and installs dependencies from `requirements.txt`.

3. **Start JupyterLab**:
   ```bash
   start
   ```
   Opens JupyterLab in your default browser at `http://localhost:8888`. Use `tmux attach -t jupyter` to view the server logs.

4. **Stop JupyterLab**:
   ```bash
   stop
   ```

## Example `requirements.txt`

Here’s a sample to get you started with data science and AI tools:

```
httpx
jupyter-ai[all]
jupyterlab
nbstripout
numpy
pandas
requests
```

## Why UV?

- **Speed**: Significantly faster than `pip` and `virtualenv`.
- **Simplicity**: Combines venv creation and package management in one tool.
- **Trendy**: Adopted by cutting-edge AI projects like MCP and OpenManus.

## Structure

- `flake.nix`: Defines the Nix Flake with `uv`-powered Python environment.
- `requirements.txt`: Your Python dependencies (customize as needed).
- `.gitignore`: Ignores `flake.lock` and `.venv` for clean commits.

## Customization

- **Add Packages**: Edit `requirements.txt` and re-run `nix develop`.
- **CUDA**: Automatically enabled on Linux if `nvidia-smi` is detected.
- **OS-Specific Tweaks**: The flake adapts to Linux or macOS automatically.

## Troubleshooting

- **No browser tab?** Visit `http://localhost:8888` manually.
- **Dependency errors?** Check `requirements.txt` syntax or run `uv pip install -r requirements.txt` manually inside the shell.
- **CUDA not working?** Ensure NVIDIA drivers and `nvidia-smi` are installed.

## Contributing

Feel free to fork, submit issues, or send pull requests! This is a community-driven starting point for modern Python workflows with Nix.

## Credits

Built with insights from exploring AI platforms and modern dev tools, with a little help from Grok 3 by xAI.

## License

MIT © 2025 [Mike Levin](https://github.com/miklevin)
