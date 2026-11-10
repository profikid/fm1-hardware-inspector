# FM-1 Hardware Inspector

A conservative, read-only v1 single-page utility for reviewing M-VAVE FM-1 hardware reports and known compatibility risks.

## Live site

https://profikid.github.io/fm1-hardware-inspector/

## What v1 does

- Displays device details from a locally selected JSON report.
- Identifies two reported 1 MiB SPI flash variants: Puya P25Q80H (JEDEC 0x856014) and UCUN UC25HQ80 (0xB36014).
- Separates unknown, experimental, incompatible and verified claims.
- Warns when bootloader identity is unknown, unreadable or missing.
- Explains why newer flash IDs require firmware and update-loader support.
- Keeps report processing in the browser; no report upload or telemetry.

## Important limitation

**Direct USB flash inspection is not implemented in browser-only v1.** FM-1 inspection through JieLi AC791N download mode uses a mass-storage/vendor-SCSI protocol. Browser WebUSB cannot reliably claim and operate that interface across operating systems. The page deliberately does not show a fake live scan or infer hardware from a USB chooser.

A future release can add a separately installed, auditable local helper based on the M-Flasher protocol. Until then, load a report produced by a trusted inspection workflow. The report schema is documented in report.schema.json.

## Safety

This project does not contain flash-write, erase, firmware-update, bootloader-install or recovery controls. Never treat unknown as verified. An unreadable bootloader is not necessarily absent. Keep an untouched full-flash backup before any future modification; backups may contain Bluetooth pairings, calibration, settings and user data.

The newer UCUN flash variant has been reported to be rejected by older firmware that checks only the Puya JEDEC ID. A black-screen incident has also been reported with an m-bootloader/newer-chip combination, while later testing on another unit succeeded. These reports justify caution, not a universal claim that the chip or bootloader is inherently incompatible.

## References

- [M-Flasher](https://github.com/jvitkauskas/m-flasher) — inspection, backup, flash map and JieLi download-mode tooling.
- [M-Flasher issue #13](https://github.com/jvitkauskas/m-flasher/issues/13) — reported m-bootloader black-screen incident on a newer-chip unit.
- [Firmware Hub](https://github.com/firmware-hub) — firmware and recovery resources.
- [MvaveFM1Unbricker](https://github.com/JustMikeR/mvave-fm1-unbricker) — device recovery project.

## Development

No build step or package installation is required. index.html is the complete static app. Open it locally or publish it with the included GitHub Pages workflow.

## License

MIT. This is an independent community project and is not affiliated with M-VAVE.
