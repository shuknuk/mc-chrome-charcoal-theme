# Minecraft × Charcoal

> [!IMPORTANT]
> **Installing on macOS:** A GitHub ZIP is source code, not a drag-and-drop Chrome installer. Chrome on macOS also restricts installing locally distributed `.crx` files. The supported route is **Chrome → chrome://extensions → Developer mode → Load unpacked** and select the extracted folder with `manifest.json`. The wallpaper at `images/minecraft-lagoon.png` must be included. **It is currently missing from this repository**, so a GitHub ZIP alone does not yet work. Use the separately distributed complete source ZIP until the original PNG is uploaded here.
>
> To create a packaged `.crx` from the complete source on your Mac, open `chrome://extensions`, enable Developer mode, click **Pack extension**, and select the theme folder. Chrome will write a `.crx` and a private `.pem` key. **Never commit or distribute the `.pem` file.** The `.crx` is a real package, but macOS Chrome may refuse direct drag-and-drop installation. A Chrome Web Store listing is the standard one-click installation method for other users.


A Chrome theme I made because most dark themes were either too gray or had a blue tint I didn't want. This one sticks to neutral blacks and charcoal, with my Minecraft lagoon screenshot on the new tab page.

The browser stays out of the way. The wallpaper gets to be the colorful part.

> **Wallpaper file:** This repository expects `images/minecraft-lagoon.png`. Until that image is uploaded, the theme cannot be installed from a GitHub ZIP. The original image is included in the [local theme package](https://github.com/shuknuk/mc-chrome-charcoal-theme) once added here.

## Install

1. Once `images/minecraft-lagoon.png` appears in the repository, download it as a ZIP using **Code → Download ZIP**, or clone it.
2. Extract the ZIP. Chrome needs the folder, not the ZIP itself.
3. Open `chrome://extensions`.
4. Turn on **Developer mode** in the upper-right corner.
5. Click **Load unpacked** and select the folder containing `manifest.json`.
6. Open a new tab.

Keep the extracted folder somewhere permanent. If you move or delete it, Chrome might have trouble loading the local theme later.

To remove the theme, open `chrome://settings/appearance` and choose **Reset to default**.

## Colors

These are the **original v1.0 values**, taken from `manifest.json`. If you want to make a variant, start here instead of sampling a screenshot. The hexadecimal codes and RGB triplets below describe the same colors.

| Part | Hex | RGB | What it does |
| --- | --- | --- | --- |
| Frame | `#090909` | `9, 9, 9` | Near-black strip around the tabs. This is the main color of the theme. |
| Inactive window frame | `#101010` | `16, 16, 16` | Slightly lighter frame when Chrome isn't the focused window. |
| Toolbar | `#171717` | `23, 23, 23` | Charcoal bar behind the address bar and browser controls. |
| Background/inactive tab | `#242424` | `36, 36, 36` | Subtle gray for inactive tabs, if supported by the installed Chrome version. |
| Button background | `#242424` | `36, 36, 36` | Background color specified for theme buttons. |
| Address bar background | `#292929` | `41, 41, 41` | Gives the address field a little separation from the toolbar. |
| Active tab text | `#F5F5F5` | `245, 245, 245` | Soft white, not full `#FFFFFF`. |
| Inactive tab text | `#A3A3A3` | `163, 163, 163` | Muted so inactive tabs don't pull your attention. |
| Bookmark text | `#D4D4D4` | `212, 212, 212` | Off-white bookmarks. |
| Toolbar icons | `#D4D4D4` | `212, 212, 212` | Back, refresh, and other supported browser controls. |
| Toolbar text | `#EBEBEB` | `235, 235, 235` | Light text against the charcoal toolbar. |
| Address bar text | `#F5F5F5` | `245, 245, 245` | High contrast in the address field. |
| New tab text | `#F5F5F5` | `245, 245, 245` | Text on the new tab page, where Chrome applies it. |
| New tab links | `#D4D4D4` | `212, 212, 212` | Softer link color. |
| New tab header | `#171717` | `23, 23, 23` | Matches the toolbar. |

### Why these particular shades?

The frame is almost black, but not pitch-black. The toolbar is only a little lighter, so you can tell where the tab strip ends without seeing a hard divider. Inactive tabs sit at `#242424`. The address bar uses `#292929` to keep its shape visible.

All of the grays are **neutral**: red, green, and blue have equal values. There's no blue cast or warm tint. Text is slightly softer than pure white, and inactive tab labels are dimmer than the active one.

**The five colors to keep handy**

```text
Frame          #090909
Toolbar        #171717
Inactive tabs  #242424
Address bar    #292929
Main text      #F5F5F5
```

A useful rule if you edit the theme: keep the frame darkest, the toolbar one step lighter, and the address field slightly lighter again. You don't need a bright accent color.

## Wallpaper

The expected file at `images/minecraft-lagoon.png` is the original **2048 × 1152** Minecraft screenshot, without recoloring, blurring, or cropping.

The manifest requests centered alignment and no repetition:

```json
"properties": {
  "ntp_background_alignment": "center center",
  "ntp_background_repeat": "no-repeat"
}
```

Chrome can still crop or position the wallpaper differently based on the window size and new-tab layout. That's browser behavior, not an edit to the image.

If you fork this for your own setup, replacing `images/minecraft-lagoon.png` with another image at the same path is enough. Keep the filename or update the `theme_ntp_background` entry in `manifest.json`.

## How the theme works

This is a native Chrome **theme**, packaged with a Manifest V3 `manifest.json` and one image. It isn't a regular browser extension that runs scripts. There are no content scripts, background processes, network requests, or permissions.

```text
mc-chrome-charcoal-theme/
├── manifest.json
├── README.md
├── .gitignore
└── images/
    └── minecraft-lagoon.png
```

Chrome reads the `theme.colors`, `theme.tints`, and `theme.properties` sections when loading it. RGB arrays use whole numbers from 0 to 255.

The original tint setting is:

```json
"tints": {
  "buttons": [-1, -1, -1]
}
```

Here, `-1` means leave that tint component unchanged. The explicit `toolbar_button_icon` color is also set to `#D4D4D4`.

**A Chrome limitation worth knowing:** the theme API doesn't give complete control over every part of the UI. Some color keys, including `background_tab`, may be ignored on newer Chrome builds. Chrome also decides tab shape, hover effects, and parts of the omnibox styling. So the manifest is the source of truth for the requested colors, but the final rendering can differ across Chrome versions and operating systems. Custom new-tab extensions can override how the wallpaper appears.

## Editing the palette

Open `manifest.json`, find `theme.colors`, and edit the relevant RGB triplet. For example, the original toolbar is:

```json
"toolbar": [23, 23, 23]
```

That is `#171717`. Reload the theme from `chrome://extensions` to see your changes. If Chrome doesn't update right away, remove the theme and load the folder again.

For color conversion, each two-digit hex pair becomes one decimal value. `#292929` is `[41, 41, 41]`.

## Version history

### 1.0.0

The original Minecraft × Charcoal theme. Neutral near-black frame, charcoal toolbar, muted tab labels, and the untouched Minecraft lagoon wallpaper. This is the version I kept after trying a brighter Windows 11-inspired gray palette.

## Notes

- The source wallpaper is part of this personal theme. Please don't assume it's separately licensed as a stock image.
- There's no Chrome Web Store listing here. Installation uses **Load unpacked**.
- If Chrome says **Could not unzip extension for install**, you probably selected the ZIP instead of the extracted folder.
