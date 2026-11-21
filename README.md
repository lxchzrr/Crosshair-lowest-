# MinimalCrosshair

Ultra-lightweight native Windows crosshair overlay written in pure **C++17** with zero GPU framework overhead (`~1.5 - 2.5 MB` RAM in idle, `0%` CPU during gameplay).

## Highlights

- **Zero Direct2D / D3D11 / WebView Overhead:** Renders directly on the CPU into a compact `144x144` 32-bit premultiplied DIB buffer using Signed Distance Fields (SDF) with 16x subpixel anti-aliasing and `UpdateLayeredWindow`.
- **On-Demand UI Lifecycle:** Closing the settings window (`[X]`) destroys all UI controls, fonts, and preview buffers to free memory while keeping the overlay active in the system tray.
- **Click-Through & Topmost:** Uses `WS_EX_LAYERED | WS_EX_TRANSPARENT | WS_EX_TOPMOST | WS_EX_NOACTIVATE` for borderless and windowed games without stealing focus.
- **Live Customization:** 5 presets (*Dot, Cross, Circle + Dot, T-Cross, X-Mark*), custom RGB color picker, opacity, length, thickness, center gap, outline, X/Y offset, and multi-monitor switching.
- **Instant Toggle & Persistence:** Press `INSERT` globally to show/hide the crosshair; settings auto-save to `crosshair.ini`.

