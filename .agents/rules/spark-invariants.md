# ⚡ Spark Workspace Rules & Architectural Invariants

> **Project**: Spark (Sub-10ms Native Rust Ephemeral Thought Capture HUD)  
> **Framework**: Native Rust (LLVM) / Windows Subsystem  
> **Author**: Karan Singh Verma

---

## 🏛️ Core Principles & Invariants

### 1. ⚡ Zero Background Daemon Invariant (0 MB Idle Footprint)
- **Summon-On-Demand**: Spark lives strictly while typing (`Ctrl + Alt + S`).
- **Complete Dismissal**: Pressing `Esc` or `Ctrl+Enter` terminates the process completely, returning idle memory consumption to **0 MB RAM** and **0% CPU**.
- **No Background Services**: Never introduce persistent background worker threads or system tray watchers.

### 2. 🦀 Sub-10ms Cold Launch & Single-Binary Architecture
- **Performance Budget**: Cold startup to first frame must remain under 10ms.
- **LLVM Single-File Binary**: Production artifact compiles to a single, standalone binary (~3 MB) deployed to `~/.local/bin/Spark.exe`.
- **Zero Heavy Web Wrappers**: Strictly forbidden from using Electron, Tauri webviews, or heavy GUI runtimes.

### 3. 🎯 Single-Instance Win32 Mutex & Workspace Teleportation
- **Mutex Guard**: Enforce `CreateMutexW` (`Local\Spark_SingleInstance_Mutex`) to ensure strictly one running instance at any time.
- **Virtual Desktop Teleportation**: If summoned while already running on a different virtual desktop, use Win32 `SetForegroundWindow` and `SetWindowPos` to teleport the canvas to the operator's current workspace and focus the text buffer immediately.

### 4. 📝 Atomic Thought Flush & Smart Formatting
- **Atomic Append**: Thought flushes to `~/.gemini/Spark.md` must be atomic and UTF-8 encoded with standard ISO/IST timestamp headers.
- **Smart Bullet Engine**: Automatically prepend markdown list items (`* `) while preserving intentional indentation and multi-line thoughts.

### 5. 🎨 Void Black Visual Language (#0A0C10)
- **Immersion**: Void Black backdrop (`#0A0C10`) with dynamic amber border glow (`#D97706`), clean sans typography, and zero jarring borders.
- **High-DPI Awareness**: DPI-aware rendering with crisp subpixel typography across 100%, 125%, and 150% Windows scaling factors.

### 6. 🛣️ Zero Absolute Machine Path Invariant
- **Dynamic Home Expansion**: Use `dirs::home_dir()` or `%USERPROFILE%` dynamically. Never commit machine-specific paths.
