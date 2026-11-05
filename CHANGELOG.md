# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Released]

## [2.1.0] - 2026-11-05

### Added
- **Nix Rpath Shim**: Added `nix() { LD_LIBRARY_PATH="" command nix "$@"; }` to `baseEnvSetup` so child `nix` invocations inside `.#default` and `.#quiet` shells never collide with `LD_LIBRARY_PATH`
- **2026 Architecture Note**: Linked `README.md` to the pure-`pip` sibling (`pipulate/levinix`) and the full production Software Von Neumann Probe (`pipulate/pipulate`)

### Fixed
- **Darwin & Nixpkgs Compatibility (PR #1 by `@nolith`)**: Replaced deprecated `python313Full` with `python313` and wrapped `CUDA_HOME` / `cudatoolkit` setup in `pkgs.lib.optionalString pkgs.stdenv.isLinux` so `aarch64-darwin` evaluations succeed cleanly

## [2.0.0] - 2025-01-03

### Added
- **Multiple Shell Support**: Added support for different shell environments to serve different use cases
  - Default interactive shell (`nix develop` or `nix develop .#default`) with full banners and verbose feedback for human developers
  - Quiet shell (`nix develop .#quiet`) with minimal output designed for AI assistants and automation tools
- **Cross-Platform Shell Functions**: Created `mkLinuxShells` and `mkDarwinShells` functions for better OS-specific shell management
- **Base Environment Setup**: Extracted common environment setup into `baseEnvSetup` function for consistency
- **Enhanced Documentation**: Added detailed comments in `flake.nix` explaining the multi-shell architecture

### Changed
- **Refactored Shell Architecture**: Completely restructured shell creation from single shells per OS to multiple shell variants per OS
- **CUDA Detection**: Moved CUDA environment variable setup to base function while keeping user messages in interactive shell only
- **Flake Output Structure**: Changed from single `devShell` to `devShells` (plural) while maintaining backward compatibility

### Technical Details
- The quiet shell eliminates verbose banner output that can clutter AI assistant context windows
- Both shells maintain identical functionality and environment setup
- CUDA support remains automatic but with context-appropriate messaging
- Backward compatibility preserved - existing `nix develop` commands continue to work

### Migration Notes
- No breaking changes for existing users
- `nix develop` continues to work as before (defaults to interactive shell)
- New users can choose `.#quiet` for automation and AI assistant workflows

## [1.0.0] - 2025-01-02

### Added
- Initial release with `uv`-based Python environment
- Cross-platform support for Linux, macOS, and Windows (WSL)
- Automatic CUDA detection and configuration
- JupyterLab integration with `start` and `stop` commands
- Virtual environment setup with `uv` instead of traditional `pip`
- Basic `requirements.txt` support

### Features
- Fast dependency installation using `uv`
- Reproducible environments via Nix Flakes
- Auto-reloading development workflow
- Modern Python 3.13 support 
