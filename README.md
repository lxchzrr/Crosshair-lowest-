# MinimalCrosshair

Ultra-lightweight native Windows crosshair overlay written in pure **C++17** with zero GPU framework overhead (`~1.5 - 2.5 MB` RAM in idle, `0%` CPU during gameplay).

## Highlights

- **Zero Direct2D / D3D11 / WebView Overhead:** Renders directly on the CPU into a compact `144x144` 32-bit premultiplied DIB buffer using Signed Distance Fields (SDF) with 16x subpixel anti-aliasing and `UpdateLayeredWindow`.
- **On-Demand UI Lifecycle:** Closing the settings window (`[X]`) destroys all UI controls, fonts, and preview buffers to free memory while keeping the overlay active in the system tray.
- **Click-Through & Topmost:** Uses `WS_EX_LAYERED | WS_EX_TRANSPARENT | WS_EX_TOPMOST | WS_EX_NOACTIVATE` for borderless and windowed games without stealing focus.
- **Live Customization:** 5 presets (*Dot, Cross, Circle + Dot, T-Cross, X-Mark*), custom RGB color picker, opacity, length, thickness, center gap, outline, X/Y offset, and multi-monitor switching.
- **Instant Toggle & Persistence:** Press `INSERT` globally to show/hide the crosshair; settings auto-save to `crosshair.ini`.

## Customizing the App Icon

Replace `icon.ico` in the root folder with your own `.ico` file (keep the exact filename `icon.ico`), then run `COMPILAR.bat`. Both `resources.rc`, the settings window, and the system tray icon automatically embed `icon.ico`.

## Build Instructions (Windows + Zig)

1. Install [Zig](https://ziglang.org/download/) (`winget install zig.zig`).
2. Run `COMPILAR.bat` (or compile manually via CLI):

```bat
zig c++ -target x86_64-windows-gnu -std=c++17 -O3 -s -fno-exceptions -fno-rtti -DUNICODE -D_UNICODE -Wl,--subsystem,windows src\main.cpp src\config.cpp src\renderer.cpp src\overlay.cpp src\settings_ui.cpp src\tray.cpp resources.rc -o MinimalCrosshair.exe -ldwmapi -luser32 -lgdi32 -lshell32 -lcomdlg32
```

## Project Structure

```text
MinimalCrosshair/
├── src/
│   ├── main.cpp          # Entry point, single-instance mutex, global hotkey & tray host
│   ├── config.h/.cpp     # INI persistence and crosshair presets
│   ├── renderer.h/.cpp   # CPU SDF 16x MSAA pixel renderer
│   ├── overlay.h/.cpp    # Topmost click-through layered overlay window
│   ├── settings_ui.h/.cpp# Custom dark-mode Win32 controls & live preview
│   └── tray.h/.cpp       # System tray integration
├── icon.ico              # Application, window, and system tray icon
├── resources.rc          # Win32 icon resource script
├── COMPILAR.bat          # One-click Zig release build script
└── .gitignore
```
