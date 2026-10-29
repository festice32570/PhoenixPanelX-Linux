# PhoenixPanelX Linux review — 2026-10-29

## Test environment
- Host: linuxreal; Zorin OS 18.1 on Ubuntu 24.04 base, kernel 7.0.0-38-generic, GNOME/X11
- Existing desktop application remained running; no privilege escalation, reboot, destructive operation or hardware control during tests.
- Python unit/synthetic regression tests: **39 tests executed and passed**, including four newly added regression tests.

## Verified fixes
1. GUI sampling now reuses the frequency measurement from the guarded metrics polling routine; failures to query CPU frequency no longer abort sensor updates or suppress possible temperature alerts.
2. Mode-change restart chooses the actual standalone executable when running a frozen PyInstaller build; Python source execution continues to use module invocation.
3. Missing/nonfinite temperature samples clear hot/debounce state without erasing the most recent warning time; this prevents an intermittent sensor dropout from circumventing the 300-second warning repeat interval. A genuine cool-down past the 5-degree hysteresis margin can still rearm alerts.
4. NVIDIA output is parsed as CSV with field-specific validity ranges. NaN, implausible temperatures, negative power/VRAM and invalid fan percentages are discarded rather than being passed to the dashboard or warning logic.
5. AMD/Intel sysfs readings also reject invalid/nonfinite values where supported.

## Scope and limitations
- Existing and new tests are synthetic or local Linux tests. They cannot prove correct operation on every motherboard, sensor driver or distribution.
- The real physical motherboard Beep mechanism and user authorization on a separate non-root workstation were not re-tested.
- Linux does not expose readings that the driver or underlying hardware does not provide. Missing temperatures remain unavailable, not guessed.
- Please review the exact binary attached to the release separately; a successful test suite is not a proof of all GUI/audio features.
- No application source code was included in the public repository. The publicly distributed executable can still be studied/reverse engineered; it is not a secrecy guarantee.
