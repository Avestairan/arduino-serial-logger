# Changelog

## v1.0.0 - 2026-06-07

### Added

- Added a real remembered-port list using `navigator.serial.getPorts()`.
- Added a `Refresh` button for updating authorized ports.
- Added `CHANGELOG.md`.
- Added complete Persian documentation explaining why this project was created.
- Added explanation of the Arduino IDE 2.x Serial Monitor copying limitation.
- Added troubleshooting, privacy, browser support and known limitation sections to `README.md`.

### Changed

- Improved connect/disconnect handling.
- Improved reader cleanup before closing the serial port.
- Improved serial command sending by using `TextEncoder` directly with `serialPort.writable.getWriter()`.
- Improved serial line parsing for `\n`, `\r`, and `\r\n`.
- Updated the license copyright holder.
- Expanded and reformatted `README.md`.

### Fixed

- Fixed the confusing static port selector.
- Fixed a possible port-lock issue after disconnecting.
