# gbdk-minimal-template
A minimal project template for GB development using GBDK-2020 and CMake.

## Requirements
- Windows 11 or Ubuntu 24.04
- GBDK-2020 >= 4.5.0
- CMake >= 4.2.1
- GNU Make >= 4.4.1

**TIPS:**
- **Windows:** Use [Chocolatey](https://community.chocolatey.org/) to install dependencies: `choco install cmake make`
- **Ubuntu:** Use apt to install dependencies: `sudo apt install cmake make`

## Build Instructions

### Prerequisites
Edit `CMakeLists.txt` and set `GBDK_HOME` to point to your extracted GBDK path.

Examples:
- **Windows:** Extract GBDK-2020 to `C:\gbdk` and set `set(GBDK_HOME "C:/gbdk")`
- **Ubuntu:** Extract GBDK-2020 to `~/dev/gbdk` and set `set(GBDK_HOME "~/dev/gbdk")`

### Quick Build

**Windows (PowerShell):**
```powershell
.\build.ps1
```

Optional flags:
- `-clean` - Clean build artifacts before building
- `-debug` - Build in debug mode

Example:
```powershell
.\build.ps1 -clean -debug
```

**Ubuntu (Bash):**
```bash
./build.sh
```

Optional flags:
- `clean` - Clean build artifacts before building
- `debug` - Build in debug mode

Example:
```bash
./build.sh clean debug
```

This will generate `rom.gb` in the `build` directory, which can be loaded into an emulator or flashcart.

### Manual Build
To build manually using CMake (works on both Windows and Ubuntu):

```bash
mkdir build
cd build
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release
make
cd ..
```

Use `-DCMAKE_BUILD_TYPE=Debug` for debug build.

## Custom Compiler Flags

You can customize the ROM build by modifying the `CUSTOM_FLAGS` variable in `CMakeLists.txt`:

```cmake
# Custom flags for lcc
set(CUSTOM_FLAGS "")
```

### Common Flags

| Flag | Description |
|------|-------------|
| `-Wm-yn"TITLE"` | Set ROM title (max 15 characters) |
| `-Wm-yc` | Enable GB Color compatible mode |
| `-Wm-yC` | GB Color only mode |
| `-Wm-ys` | Enable Super GB mode |
| `-Wm-yoA` | Automatic ROM bank size |
| `-Wm-yo<N>` | Set number of ROM banks (2, 4, 8, 16, 32, 64, 128, 256, 512) |
| `-Wm-ya<N>` | Set number of 8K SRAM banks (0, 1, 4, 16) |
| `-Wm-yt<N>` | Set MBC cartridge type (e.g., `0x1A` for MBC5 with SRAM) |
| `-Wm-yS` | Generate `.sym` symbol file for emulator debugging |

### Examples

Set ROM title:
```cmake
set(CUSTOM_FLAGS "-Wm-yn\"MYGAME\"")
```

GB Color with automatic banking:
```cmake
set(CUSTOM_FLAGS "-Wm-yc -Wm-yoA")
```

MBC5 with 32K SRAM and 64 ROM banks:
```cmake
set(CUSTOM_FLAGS "-Wm-yt0x1A -Wm-yo64 -Wm-ya4")
```

For more details, see the [GBDK Documentation](https://gbdk.org/docs/api/docs_faq.html#autotoc_md219) and [ROM Banking Guide](https://gbdk.org/docs/api/docs_rombanking_mbcs.html#autotoc_md90).

## Resources
- GBDK: https://github.com/gbdk-2020/gbdk-2020
- Getting Started With GBDK Tutorial: https://laroldsretrogameyard.com/tutorials/gb/getting-started-with-gbdk-2020/
