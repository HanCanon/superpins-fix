# SuperPins Fix

[English](README.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md)

**Final version: 0.1.2** · [Install with Sine](https://github.com/CosmoCreeper/Sine) · [Report an issue](https://github.com/HanCanon/superpins-fix/issues)

An independent CSS patch for [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins) in [Zen Browser](https://zen-browser.app/), installed alongside the original mod through Sine. It fixes overflowing audio controls, misplaced Glance indicators, and favicons that are off-center within pinned-tab backgrounds.

## Features

- **Centered favicons:** website icons stay horizontally and vertically centered within the tab background, including during audio playback and Glance previews.
- **Floating previews:** Glance appears as a small card in the upper-right corner, with a background and border inspired by Zen Essentials.
- **Audio badges:** the lower-right audio button retains native mute, unmute, and state handling.
- **Preserved layout:** no increased minimum tab width; SuperPins spacing and wrapping are retained.
- **Independent installation:** CSS only, with no additional JavaScript. No edits to SuperPins files or Sine-generated stylesheet entries are required.

## Installation

1. Install and enable [Sine](https://github.com/CosmoCreeper/Sine) and the original **SuperPins** mod.
2. Enable Zen's vertical tabs and SuperPins' **legacy layout** (icon grid) and **auto-grow** options.
3. Enter the following in Sine's custom GitHub repository installation field:

   ```text
   HanCanon/superpins-fix
   ```

4. Install and enable **SuperPins Fix**, keeping SuperPins enabled as well. Restart Zen if the styles do not refresh.

If you have an older patch installed, check for updates in Sine and confirm version **0.1.2**. Do not import the project folder or `theme.json`; Sine's Import button restores an exported mod list.

## Compatibility and required settings

| Component | Verified version |
| --- | --- |
| Zen Browser | 1.22.2b |
| SuperPins | 1.7.2 |
| Sine | 2.3.4.1c |

Check these preferences in `about:config`:

| Preference | Required value |
| --- | --- |
| `zen.tabs.vertical` | `true` |
| `uc.pins.legacy-layout` | `true` |
| `uc.pins.auto-grow` | `true` |

The patch applies only to **top-level pinned-tab grids in the expanded sidebar**. Regular tabs, Essentials, and tabs inside folders are outside its scope. The patch layout does not apply when the required settings are disabled or the pinned area contains a drag-target marker.

Compatibility with other versions is unconfirmed. On multiple devices, install the patch separately and use the same required settings; this project does not synchronize browser preferences.

## Validation and limitations

Version 0.1.2 passed isolated layout and native interaction tests. The maintainer has also confirmed satisfactory results in daily use, with no further issues observed so far.

- Tested 24 layout combinations covering normal, playing, muted, and blocked-media states, with and without Glance. Actual audio mute/unmute, Glance opening/closing, and their combined interaction were tested separately.
- At pinned-area widths of 180, 240, 260, and 320 CSS px, tab dimensions, positions, and wrapping were unchanged by the patch. Favicons were corrected to the background center.
- Tested with 16px favicons and 40px tab height. The audio control and its clickable area are 16px; the Glance card is 24×20px with a 14px icon.
- On narrow tabs, the preview card may overlap the favicon's edge. This layering is intentional and does not move the favicon. Audio and Glance badges occupy separate lower and upper corners without covering each other.
- Other icon/tab sizes, resuming genuinely blocked autoplay, the Alt-click gesture, compact-sidebar hide/reveal behavior, and the complete remote update flow have not been fully verified.

## Removal and troubleshooting

Disable or uninstall **SuperPins Fix** in Sine to restore the original appearance. No other configuration files need restoring.

If the patch is not applied, check component versions, the three required preferences, and that both mods are enabled in Sine, then restart Zen. For visual issues, compare with the patch disabled and check other mods that change tab appearance. If upstream fixes these issues, disable this patch to determine whether it is still needed.

## Project status and feedback

**0.1.2 is the final version. No further releases are planned.** Future Zen, SuperPins, or Sine updates may affect compatibility; ongoing adaptation is not promised.

You may still document problems in [Issues](https://github.com/HanCanon/superpins-fix/issues), but responses and fixes are not guaranteed. Include component versions, SuperPins settings, sidebar mode, other relevant mods, reproduction steps, and screenshots with the patch enabled and disabled.

## Project files

| File | Purpose |
| --- | --- |
| [chrome.css](chrome.css) | CSS patch |
| [theme.json](theme.json) | Sine metadata |
| [README.md](README.md) | English guide |
| [README.zh-CN.md](README.zh-CN.md) | Simplified Chinese guide |
| [README.ja.md](README.ja.md) | Japanese guide |

## Credits

[Zen Browser](https://github.com/zen-browser/desktop) · [SuperPins](https://github.com/CosmoCreeper/Zen-Themes/tree/main/SuperPins) · [Sine](https://github.com/CosmoCreeper/Sine)

This is an independent compatibility patch, not an official component of the projects above.
