<div align="center">

# 🕐 Nixie Clock Card

**A nixie tube clock for Home Assistant: six IN-14 tubes with glowing gas, cyan underlights and an acrylic base, rendered in WebGL.**

[![HACS Custom][hacs-badge]][hacs-url]
[![Release][release-badge]][release-url]
[![Validate][validate-badge]][validate-url]
[![License: MIT][license-badge]][license-url]

[![Open your Home Assistant instance and open this repository in HACS.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=cerealkiller57540&repository=nixie-clock-card&category=plugin)

<img src="https://raw.githubusercontent.com/cerealkiller57540/nixie-clock-card/main/images/main.gif" alt="Nixie Clock Card: six glass tubes with orange glowing digits and cyan LEDs at their feet" width="600">

</div>

The WebGL card is drawn after a real desk nixie clock: six separate IN-14 tubes, orange digits behind a fine wire mesh, a cyan LED at the foot of each tube, two-dot LED separators and a black acrylic base. The gas flickers, unlit digits show faintly through the glass, and each change cross-fades from one digit to the next.

<img src="https://raw.githubusercontent.com/cerealkiller57540/nixie-clock-card/main/images/variants.png" alt="The CSS card (left) and the WebGL card (right), without any theme" width="800">

*Left: `nixie-clock-card` (CSS, wooden-case look with screws). Right: `nixie-clock-card-webgl`. No theme.*

## ✨ Features

- **Two cards in one install**
  - `nixie-clock-card-webgl`: glass tubes, gas glow and LEDs rendered by a WebGL shader (recommended).
  - `nixie-clock-card`: a different take, a framed display drawn with CSS, with colour presets.
- **No entity needed**: it reads your device clock.
- **12 h or 24 h**, with or without seconds (6 or 4 tubes).
- **Underlights follow your theme's accent colour** by default.
- **Full visual editor** on the WebGL card: every glow, glass and LED setting is a slider, applied live.
- Pauses when off-screen, releases its WebGL context when removed (Android WebViews cap a page at 8 contexts), respects `prefers-reduced-motion`.
- A small ghost cat called Glitch shows up now and then. Turn it off with `glitch: false`.

## 📦 Installation

### HACS (recommended)

1. Click the **Open in HACS** button above, or add this repository as a custom repository in HACS (category **Dashboard**): `https://github.com/cerealkiller57540/nixie-clock-card`.
2. Download **Nixie Clock Card**.
3. Reload your browser.

HACS registers one resource, `nixie-clock-card.js`. It loads the WebGL variant on its own, so **do not** add `nixie-clock-card-webgl.js` as a second resource.

### Manual

1. Copy both files from [`dist/`](dist) to `config/www/nixie-clock-card/`.
2. Add a dashboard resource: URL `/local/nixie-clock-card/nixie-clock-card.js`, type **JavaScript module**.

## 🚀 Usage

```yaml
type: custom:nixie-clock-card-webgl
```

That is all it needs. With a few options:

```yaml
type: custom:nixie-clock-card-webgl
use_military: false      # 12 h
hide_seconds: true       # 4 tubes
under_color: "#ff2d6b"   # LEDs and separators
```

## ⚙️ Options

**Both cards**

| Option | Type | Default | Description |
|---|---|---|---|
| `use_military` | bool | `true` | 24 h format |
| `hide_seconds` | bool | `false` | Hide the seconds (4 tubes instead of 6) |
| `glitch` | bool | `true` | The ghost cat |
| `glitch_color` / `glitch_opacity` | colour / number | card colour / `0.8` | Its colour and maximum opacity |
| `glitch_dur` / `glitch_gap` | number | `2400` / `25` | Length of one appearance (ms), average gap between two (s) |

**WebGL card** (`nixie-clock-card-webgl`)

| Option | Default | Description |
|---|---|---|
| `under_color` | theme accent | LEDs at the foot of the tubes and separators |
| `glow` / `glow_r` | `1.20` / `10.0` | Orange halo intensity and radius (px) |
| `core` | `0.35` | How much the digit stroke turns yellow-white |
| `flicker` / `flk_core` | `0.26` / `0.00` | Gas flicker, and how much of it reaches the digit itself (`0` = steady digit, only the halo breathes) |
| `ghost` | `0.12` | Visibility of unlit digits and the mesh |
| `fade` | `180` | Cross-fade between two digits (ms) |
| `under` / `under_h` | `1.00` / `0.45` | Underlight intensity, and how high the cyan climbs in the tube |
| `glass` | `0.35` | Reflections on the tube edges |
| `sep` / `sep_core` | `1.05` / `1.20` | Separator LED intensity and their white-hot centre |
| `base_refl` | `0.75` | Edge and gradient of the acrylic base |
| `glitch_size` / `glitch_sep` / `glitch_x` / `glitch_y` | `30` / `2` / `0` / `0` | Cat size, which separator it sits on, offset in px |

**CSS card** (`nixie-clock-card`)

| Option | Default | Description |
|---|---|---|
| `tube_color` | `orange` | Preset `orange`, `cyan`, `violet`, `green`, `blue`, `white`, or a CSS filter such as `hue-rotate(120deg) saturate(1.4)` |
| `glow_color` / `glow_soft` / `glow_cold` | `#ff6a00` / `#ff4500` / — | Inner glow, outer glow, cold ambient shadow |
| `case_color` / `case_border` / `screw_color` | `#0d0d0d` / `#3a2810` / border | Case colours |
| `screws` | `true` | Corner screws |
| `label` | — | Text under the clock |
| `glitch_size` / `glitch_right` / `glitch_top` | `64` / `-26` / `-40` | Cat size and position (negative = overflows the card) |

## ❓ FAQ

**The WebGL clock stays blank.** Your browser has no WebGL. Use `nixie-clock-card`, which needs none.

**Some cards go blank on my Android phone.** Android WebViews keep at most 8 WebGL contexts per page and drop the oldest one. This card uses one and gives it back when it leaves the page. If you run many WebGL cards on one view, use `nixie-clock-card` on some of them.

**Which theme is in the screenshots?** Neo Tokyo, from [Home-Assistant-Neon-Cards](https://github.com/cerealkiller57540/Home-Assistant-Neon-Cards). The card works with any theme.

## 🎨 Credits

The nixie tube digit images embedded in both cards are **© 2007-08 Cestmir Hybl** ([DHTML Nixie Display](http://cestmir.freeside.sk/projects/dhtml-nixie-display)), *free for non-commercial use, copyright must be preserved*. They are **not** covered by the MIT licence of this repository's code (see [NOTICE](NOTICE.md)). The Glitch cat silhouette comes from [openclipart](https://openclipart.org) (public domain).

## 🌃 More neon cards

This card is part of a family. See the full collection at [**Home-Assistant-Neon-Cards**](https://github.com/cerealkiller57540/Home-Assistant-Neon-Cards).

---

## 🐾 Support this project

If you enjoy these cards, please consider donating to **Quatre Pattes**, an animal rescue organization.

[![Sauver des animaux](https://img.shields.io/badge/🐾%20Sauver%20des%20animaux-Faire%20un%20don-ff69b4?style=for-the-badge)](https://don.quatre-pattes.org/s/?_jtsuid=70083177244599792679303)

> 💛 No need to support me — just help the animals. Thank you!

---

## 🤝 Contributing

1. Fork the repo
2. Create your branch: `git checkout -b feature/my-card`
3. Commit and push
4. Open a Pull Request

---

## 📄 License

[MIT License][license-url]

[hacs-badge]: https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge
[hacs-url]: https://hacs.xyz
[release-badge]: https://img.shields.io/github/v/release/cerealkiller57540/nixie-clock-card?style=for-the-badge
[release-url]: https://github.com/cerealkiller57540/nixie-clock-card/releases
[validate-badge]: https://img.shields.io/github/actions/workflow/status/cerealkiller57540/nixie-clock-card/validate.yml?branch=main&label=HACS&style=for-the-badge
[validate-url]: https://github.com/cerealkiller57540/nixie-clock-card/actions/workflows/validate.yml
[license-badge]: https://img.shields.io/github/license/cerealkiller57540/nixie-clock-card?style=for-the-badge
[license-url]: LICENSE
