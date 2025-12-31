# Sensory

>A compact Rust GUI for monitoring system sensor readings (lm-sensors).

Sensory displays temperature, fan speeds, voltages and other readings reported by the `sensors` command in a lightweight, refreshable GUI built with `iced`.

**Key features**
- **Live refresh:** updates readings every ~500ms by default.
- **Structured display:** groups sensors into sections with adapter info and per-entry values.
- **Lightweight GUI:** built with `iced` for a modern, cross-platform Rust UI.
- **Robust parsing:** uses `regex` and `once_cell` for reliable extraction of `sensors` output.

**Project Overview**

`sensory` is a small Rust application that runs the system `sensors` command (from the lm-sensors project), parses its output, and presents the results in a simple GUI. It is intended as a convenient desktop viewer for people who want a focused, native GUI for sensor readings.

The application is opinionated and minimal: it relies on the presence of the `sensors` executable and focuses on a clear presentation rather than advanced graphing or persistence. The code is intentionally compact and easy to extend.

**Requirements**
- `rust` and `cargo` (latest stable toolchain recommended)
- `sensors` (installed via `lm-sensors`) and accessible in `PATH`
- Linux (tested on Debian/Ubuntu; the app depends on the `sensors` command)

Install `lm-sensors` on Debian/Ubuntu:

```
sudo apt update
sudo apt install lm-sensors
```

Or for RHEL/Fedora:
```
sudo dnf update
sudo dnf install lm_sensors
```

After detection, verify `sensors` prints data:

```
sensors
```

You should see output with sensor chips, adapters, and readings.


**Build & Run**

- Debug (development): `cargo run`
- Release (optimized):

```
cargo build --release
./target/release/sensory
```

The GUI launches a single window and automatically refreshes the sensor data on a short interval. If `sensors` cannot be executed or returns no data, the UI will display an error message.

**Usage**

- The application automatically queries `sensors` once on startup and periodically thereafter (every 500ms by default).
- Sensor sections are grouped by chip name; each entry shows the key, value (with units when available), and optional additional info.
- To check raw data or debug parsing, run `sensors` in a terminal and compare output with the UI.

**Development**

- Code lives in `src/main.rs` and is structured around an `iced::Application` implementation named `SensorViewer`.
- Parsing logic is implemented in `parse_sensor_output` and tested by running `sensors` and inspecting the results.

**License**

This project is released under the MIT License — see the `LICENSE` file (or the `license` field in `Cargo.toml`).

**Acknowledgements**

- Built with `iced` for the GUI.
- Relies on `lm-sensors` (`sensors`) for hardware readings.

**Contact & Support**

If you want help or wish to contribute, open an issue or PR in the repository. Be sure to include your OS, Rust toolchain version, and `sensors` output when relevant.