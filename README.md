# DOOM T5i / 700D

Experimental DOOM port for the Canon EOS 700D / Rebel T5i, running as a
Magic Lantern module.

This project adapts Doom550D to the Canon EOS 700D / Rebel T5i and has been
tested on real hardware with Canon firmware 1.1.5.

## Demo on real hardware

Canon EOS 700D / Rebel T5i (firmware 1.1.5) running the port on real hardware.



https://github.com/user-attachments/assets/329beb9d-8cfb-4b3a-a42c-8f11ac3d22fb


## Status

Playable on the Canon EOS 700D / Rebel T5i.

The current port provides:

- Doom gameplay, menus, saves and configuration
- T5i/700D directional controls using raw Canon press/release events
- Fire, use, menu and weapon-selection controls
- Doom music and sound effects through the camera speaker
- DIGIC V audio/DMA adaptations
- 256-color Doom palette output through the Magic Lantern 700D.115 platform
- An extra 360x240 gameplay mode displayed as exact 2x2 pixels on the
  camera's 720x480 display
- Optional debug logging
- A hidden cheat menu

The port remains experimental.

## Tested hardware

- Canon EOS 700D / Rebel T5i
- Canon firmware 1.1.5
- Magic Lantern platform: `700D.115`

The development and release-test environment uses the
`reticulatedpines/magiclantern_simplified` Magic Lantern source tree at commit:

    ed3e7c0dfacfdeaf3349dee73edf9e3621217462

Do not assume that this module is compatible with other Canon cameras,
firmware versions or Magic Lantern builds.

## Installation

Magic Lantern must already be installed and working on a compatible
Canon EOS 700D / Rebel T5i running firmware 1.1.5.

Back up the SD card before installing experimental modules.

Copy the compiled module to:

    ML/modules/doom.mo

Place authorized Doom-family IWAD files in:

    ML/DOOM/

The module detects up to 32 alphabetically sorted `.wad` files containing an
IWAD header. PWAD level and mod files are not offered as standalone games.

No commercial Doom WADs or other third-party game assets are included in this
repository.

## Controls

| Camera control | DOOM action |
| --- | --- |
| Arrow keys | Move / turn; navigate menus |
| SET | Fire; confirm in menus |
| PLAY | Use / open doors and switches |
| INFO / DISP. | Use / open; back in menus |
| Rear wheel | Previous / next owned weapon |
| MENU | Open / close the Doom menu |
| Delete / Trash x3 quickly | Open secret cheat menu |
| Q | Confirm Doom quit dialog |

Rear-wheel weapon switching may occasionally be intermittent on the current
T5i/700D build.

The inherited Doom550D zoom-based run/strafe controls are not available in
this adaptation. Unsupported Zoom In and shutter events are consumed while
DOOM owns the screen so they do not alter Canon state.

## Building

This module was successfully built against the Magic Lantern source tree
listed above.

Place or copy this repository's `module` directory inside the Magic Lantern
`modules` directory. For example:

    cp -a /path/to/doom-t5i/module /path/to/magiclantern/modules/doom_t5i
    cd /path/to/magiclantern/modules/doom_t5i
    make clean
    make

A successful build produces:

    build/doom.mo

The build requires the normal Magic Lantern ARM cross-compilation toolchain.

Magic Lantern's module build system embeds build date and build-user metadata
in the generated module. This metadata does not identify the project author.

## T5i / 700D adaptation

### Input

Doom550D originally targeted the Canon EOS 550D.

The T5i/700D port maps directional input to the raw press/release events
defined by Magic Lantern's `700D.115` platform:

- Right: `0x24` / `0x25`
- Left: `0x26` / `0x27`
- Up: `0x28` / `0x29`
- Down: `0x2a` / `0x2b`

Non-directional camera controls are handled through Magic Lantern's portable
keypress callback where appropriate.

### Display and palette

The port preserves Doom's original 256 palette indices and installs the
display palette through Magic Lantern's `700D.115` platform.

An additional fullscreen gameplay setting renders at 360x240 and maps each
game pixel to an exact 2x2 block on the 720x480 camera display.

### Audio

The T5i/700D uses DIGIC V.

The port adapts the Canon ASIF-DMA audio path so DMA buffers are accessed
uncached, allowing the audio hardware to receive freshly rendered samples.

MUS music is rendered by the inherited low-CPU software synthesizer and mixed
with Doom sound effects into the Canon audio stream.

## WADs, saves and configuration

The module creates:

    ML/DOOM/
    ML/DOOM/SAVES/
    ML/DOOM/CONFIG/

Savegames are separated using a hash of the exact IWAD filename.

New saves contain a save-format version and WAD fingerprint. Damaged or
mismatched saves are rejected instead of being loaded blindly.

## Debug logging

Debug logging is optional and disabled by default.

When enabled, diagnostic information is written to:

    ML/LOGS/DOOM550D.LOG
    ML/LOGS/DOOMRAW.LOG

The `DOOM550D.LOG` filename is retained from the upstream project for
compatibility and historical continuity.

## Secret cheat menu

During an active single-player level, press Delete / Trash three times within
1.2 seconds to open the hidden cheat menu.

It provides access to classic Doom cheats, available music and maps present in
the active IWAD.

Classic gameplay cheats retain Doom's original Nightmare restrictions.

## Known issues

- Rear-wheel weapon switching can be intermittent.
- The inherited 550D zoom-based run/strafe controls are not available.
- This is an experimental module and has only been tested for the
  Canon EOS 700D / Rebel T5i target described above.
- The compiled module should not be treated as a portable binary for other
  Canon cameras or firmware versions.

## Credits

This project is an adaptation of Doom550D.

Original and upstream work includes:

- Doom engine source by id Software
- Doomgeneric
- Chocolate Doom
- Magic Lantern
- Freedoom contributors
- Doom550D by Bas Lichtjaar <doom@lauris.nl> and contributors

Canon EOS 700D / Rebel T5i adaptation:

**Raiven Fair (@raivenfair)**

Thanks to all upstream projects and contributors whose work made this port
possible.

## License

This project is distributed under the GNU General Public License version 2
(GPL-2.0), following the upstream Doom550D project.

See `LICENSE` for the complete license text.

Third-party game assets and commercial Doom WAD files are not included.
