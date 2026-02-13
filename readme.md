# Launchpad Mini [MK3] Lightshow Studio 🎹✨

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Platform](https://img.shields.io/badge/platform-Web%20MIDI%20(Chrome%2FEdge)-orange)
![Version](https://img.shields.io/badge/version-5.2-green)

**Launchpad Mini [MK3] Lightshow Studio** is a powerful, zero-dependency web application designed to unlock the full potential of your Novation Launchpad Mini [MK3]. 

Built with **Vanilla JavaScript** and the **Web MIDI API**, this tool allows you to design intricate light patterns, trigger real-time procedural animations, scroll text, and generate raw **SysEx (System Exclusive)** commands for use in your own projects or DAW setups.

---

## 🚀 Key Features

### 🔌 Seamless Connectivity
- **Instant Pairing:** Connects directly to your hardware via the browser using Web MIDI.
- **Smart Mode Switching:** Automatically puts the device into **Programmer Mode** (`0E 01`) upon connection and restores Live Mode on exit.
- **Visual Feedback:** Interactive "Connect" button that reacts to connection state.

### 🎨 Advanced Visual Painter
Design your grid with precision using three distinct lighting modes:
- **Static:** Solid, high-contrast colors.
- **Flash:** Hardware-accelerated flashing (alternating between two colors).
- **Pulse:** Smooth, rhythmic breathing effects.
- **Full Palette:** Access to the complete Novation color palette (127 colors).

### 🕹️ Procedural Animations (14 Presets)
Includes a robust JavaScript engine with **Smart Buffer Clearing** to prevent ghosting. animation presets include:
- **Atmospheric:** *Matrix Rain, Sunset Gradient, Fade, Sparkles*
- **Rhythmic:** *Police Strobe, Heartbeat, Ripple*
- **Geometric:** *Scanline, Converge, Checkers*
- **Interactive:** *Snake Game, Loading Bar, Digital Noise*

### 🛠️ Developer Tools
- **SysEx Generator:** Every action you take generates the exact Hexadecimal code needed to replicate it programmatically.
- **Text Scroller:** Native hardware text scrolling engine support.

---

## � Visual Showcase

<p align="center">
  <img src="docs/screen1.png" alt="Main Interface" width="100%">
</p>
<p align="center">
  <em>The Main Interface: A clean, dark-themed workspace for lightshow design.</em>
</p>

<br>

<p align="center">
  <img src="docs/screen2.png" alt="Animation Controls" width="48%">
  <img src="docs/screen3.png" alt="SysEx Generator" width="48%">
</p>
<p align="center">
  <em>Left: Animation Controls & Palette | Right: Real-time SysEx Command Generator</em>
</p>

---

## �📖 Technical Documentation

This tool is built on a deep understanding of the Novation SysEx protocol. Below is a breakdown of the core command structures used, extracted from our internal skill definitions.

### 1. Connection & Mode Switching
To control the LEDs directly, the device must be in **Programmer Mode**.
- **Header:** `F0 00 20 29 02 0D` (Novation / Launchpad Mini MK3)
- **Enter Programmer Mode:** `... 0E 01 F7`

### 2. Pad Addressing
The grid uses an 8x8 XY layout in Programmer Mode:
- **Bottom Left:** `11` (11h)
- **Top Right:** `88` (58h)
- **Formula:** `(Row * 10) + Column` (Rows 1-8, Columns 1-8)

### 3. Lighting Commands (03h)
We use the efficient **Lighting (03h)** command to update LEDs.

| Type | Hex | Format | Description |
| :--- | :--- | :--- | :--- |
| **Static** | `00` | `00 <Pad> <ColorID>` | Sets a solid color (0-127). |
| **Flash** | `01` | `01 <Pad> <ColorB> <ColorA>` | Flashes between Color A and B. |
| **Pulse** | `02` | `02 <Pad> <ColorID>` | Smoothly brightens and dims the color. |
| **RGB** | `03` | `03 <Pad> <R> <G> <B>` | Direct RGB control (0-127 per channel). |

*> **Tip:** To optimize performance, the app sends batch messages containing multiple LED updates within a single SysEx string, up to the hardware limit.*

---

## ⚡ Getting Started

1.  **Hardware:** Connect your Novation Launchpad Mini [MK3].
2.  **Browser:** Use a Chromium-based browser (Chrome, Edge, Opera) for Web MIDI support.
3.  **Launch:** Open `index.html` locally or deploy to a static host.
4.  **Connect:** Click the **Plug Icon (🔌)** in the sidebar to initialize the session.

### Cloning the Repo
```bash
git clone https://github.com/toniaczlog/launchpad-mk3-lightshow-studio.git
cd launchpad-mk3-lightshow-studio
# No npm install needed - it's vanilla JS!
```

---

## 🤝 Contributing & License

Contributions are always welcome! Whether it's a new animation algorithm or a UI polish, feel free to fork and submit a PR.

This project is open-source and available under the **MIT License**.

---

<div align="center">
  <p>If you find this tool useful for your performances or development:</p>
  <a href="https://www.buymeacoffee.com/toniaczlog" target="_blank">
    <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;">
  </a>
</div>