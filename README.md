# ScalyCare West Manifest

This repository defines the official `west.yml` manifest for the ScalyCare embedded development platform.

It serves as a **manifest-of-manifests**, pulling in:

- Nordic Semiconductor's `sdk-nrf` as a dependency (with Zephyr, modules, bootloader, etc.)
- ScalyCare-specific application firmware projects (e.g., `ThermoChirp-fw`)
- Any other supporting components needed across firmware releases

This repository provides a **reproducible and scalable workspace structure** for developers working on ScalyCare firmware.

---

## 📁 Workspace Layout

After initializing and updating, the expected directory structure is:

```text
<workspace-root>/
├── .west/
├── nrf/ # Nordic SDK (sdk-nrf manifest)
├── zephyr/ # Zephyr RTOS
├── modules/ # Shared modules
├── bootloader/ # MCUboot (if imported)
├── tools/ # Nordic's tools
└── projects/
└── ThermoChirp-fw/ # ScalyCare firmware projects
```

---
## Branching Policy

This repository uses a single `main` branch for west manifest and version metadata. All updates should be reviewed and tested before pushing.
---

## 🚀 Getting Started

```bash
# Clone and initialize the workspace
west init -m https://github.com/ScalyCare/manifest --mr main <workspace-dir>
cd <workspace-dir>

# Pull in all dependencies (sdk-nrf, zephyr, modules, your firmware)
west update
```
Then configure and build your firmware project as usual with west build or CMake directly.

🧩 Project Structure
All ScalyCare application firmware projects live under:

```text
projects/<project-name>/
```

Each project may contain its own prj.conf, overlays, and CMakeLists to target Nordic boards such as nrf52dk_nrf52832.

🛠️ Maintenance Notes
Modify west.yml in this repo to add/remove/update ScalyCare projects or pin SDK revisions.

To lock all project revisions for reproducibility, use:

```bash
west manifest --freeze > west.yml.lock
```

📜 License
This repository contains no source code. It is a configuration manifest for reproducible builds. Refer to individual project repositories for licensing details.

