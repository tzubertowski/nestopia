# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build Commands

Build the libretro core:
```bash
cd libretro
make
```

Clean build artifacts:
```bash
cd libretro
make clean
```

Install the built core:
```bash
cd libretro  
make install
```

## Project Overview

This is Nestopia libretro - a cycle-accurate NES/Famicom emulator core for RetroArch and other libretro frontends. It's based on the Nestopia JG fork and includes an additional overclocking feature.

## Code Architecture

### Core Structure
- **source/core/**: Main emulator engine written in C++98
  - **api/**: Public API layer (NstApi*.hpp/cpp files) - provides clean interface to emulator functionality
  - **board/**: Memory mapper implementations for different cartridge types (hundreds of mappers supported)
  - **input/**: Input device implementations (controllers, peripherals, special devices)
  - **vssystem/**: VS System arcade hardware support
- **libretro/**: libretro API wrapper that interfaces the core with RetroArch
- **nes_ntsc/**: NTSC video filter library for authentic CRT-style rendering

### Key Components
- **NstCore.hpp**: Core type definitions, platform abstractions, and fundamental utilities
- **NstMachine.hpp**: Main machine emulation controller
- **libretro/libretro.cpp**: Primary libretro interface implementation
- **API Classes**: Each NstApi*.hpp file provides access to specific emulator subsystems (Video, Audio, Input, Machine, etc.)

### Memory Mappers (Boards)
The `source/core/board/` directory contains implementations for different cartridge memory mappers. Each mapper handles specific hardware configurations and is named after the manufacturer or board type (e.g., NstBoardMmc1.cpp for MMC1 mapper).

### Platform Support
The Makefile supports numerous platforms including Unix/Linux, Windows, macOS, mobile platforms (iOS, Android), gaming consoles (PlayStation, Xbox, Nintendo), and embedded systems.

## Development Notes

- Written in C++98 for maximum compatibility
- Uses custom type definitions (dword, word, byte) defined in NstBase.hpp
- Platform-specific optimizations controlled via compiler detection macros
- No external dependencies beyond standard C++ library (zlib support disabled in libretro build)
- Database support for game-specific fixes via NstDatabase.xml

## Special Features

- Famicom Disk System support (requires disksys.rom BIOS)
- ADPCM sample support for specific games
- Multiple video filters including NTSC simulation
- Comprehensive input device support beyond standard controllers
- Save state functionality
- Cheat system support