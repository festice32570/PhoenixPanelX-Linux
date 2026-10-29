# PhoenixPanelX Linux v0.1.0-rc7 — reliability fixes

**Release candidate / experimental binary preview** for Zorin OS 18.1 (Ubuntu 24.04 family), GNU/Linux x86_64. Application source code is **not included in the public repository**.

## Changes since rc6

- Fixed the Linux monitoring loop aborting when CPU frequency could not be read on some hardware. Sensor polling now reuses the safe, guarded CPU frequency value.
- Fixed the view-mode change restart path in frozen PyInstaller builds. Frozen executables no longer try to invoke an unsupported `-m phoenixpanelx` argument.
- Fixed the warning cooldown incorrectly resetting after a transient missing/invalid temperature sample. The 300-second repeat suppression is preserved; genuine cooling can still rearm alerts.
- Rejected invalid NVIDIA readings such as NaN, implausible temperatures, negative watts/VRAM and out-of-range percentage values. AMD/Intel sysfs GPU readings also use validity checks. Unsupported readings remain unavailable.

## Validation

- Linux source regression suite: **39 tests, all passed** (including 4 new regression tests).
- Portable PyInstaller ELF x86_64 built successfully on linuxreal; isolated GUI process remained alive until an intentional 8-second test timeout (not a full GUI interaction test).
- Physical motherboard Beep, arbitrary hardware combinations, different GPUs, Wayland and distributions outside the development host were **not** retested.

## Safety, source privacy and licensing

The normal application runs without root; do not run the full GUI as root. Optional motherboard Beep permission helper is separate, grants only the specific fixed-duration operation after admin authentication, and has not been re-tested on a separate non-root PC. No system changes are made by merely running the app. The binary is unsigned and is an experimental hardware-monitoring preview, **not** a safety-critical thermal protection system. Because it is a packaged Python executable, its contents may be inspectable despite the absence of source in the public repository.

See [2026-10-29 Linux test report](./TEST_REPORT_20261029.md) and [README](./README.md).
