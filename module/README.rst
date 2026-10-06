DOOM T5i / 700D
===============

:Author: Bas Lichtjaar <doom@lauris.nl> and contributors; T5i/700D adaptation by Raiven Fair (@raivenfair)
:License: GPL-2.0
:Summary: Experimental DOOM port for Canon EOS 700D / Rebel T5i, firmware 1.1.5.

Adaptation of Doom550D for the Canon EOS 700D / Rebel T5i.
Tested on real hardware with Canon firmware 1.1.5.

Controls
--------

* Arrows: move, turn and navigate menus
* SET: fire or confirm
* PLAY: use/open
* INFO/DISP.: use/open; back in menus
* Rear wheel: previous/next weapon
* MENU: open/close Doom menu
* Delete/Trash x3: secret cheat menu
* Q: confirm the Doom quit dialog

Rear-wheel weapon switching may be intermittent.

Files and saves
---------------

Place authorized Doom-family IWADs in ``ML/DOOM/``.
WADs and commercial game assets are not included.

Saves are stored in ``ML/DOOM/SAVES``.
Settings are stored in ``ML/DOOM/CONFIG``.

Optional debug logs are written to ``ML/LOGS``.
Debug logging is disabled by default.

Port features
-------------

Directional input uses raw ``700D.115`` press/release events.
The port preserves Doom's original 256 palette indices.

Extra fullscreen renders gameplay at 360x240 as 2x2 pixels.
DIGIC V ASIF-DMA audio uses uncached DMA buffers.

The inherited 550D zoom run/strafe controls are unavailable.

Compatibility
-------------

Target: Canon EOS 700D / Rebel T5i, firmware 1.1.5.
Magic Lantern must already be installed and working.

This module is experimental.
Do not assume compatibility with other cameras or firmware.
Back up the SD card before installing experimental modules.

T5i/700D adaptation by Raiven Fair (@raivenfair).
Doom550D by Bas Lichtjaar and contributors.
Released under GPL-2.0.
