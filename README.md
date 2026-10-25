# Vessel Motion P4 — OTA releases

Public OTA channel for the Vessel Motion P4 firmware (ESP32-P4-Nano).
Source code lives in the private repo `barba-productions/vessel-motion-p4`.

## Layout

- `stable/manifest.json` — update manifest read by the device
  (Settings → FIRMWARE → UPDATE)
- `stable/vessel_motion_p4.bin` — firmware application image

## Manifest schema (v1)

```json
{
  "schema": 1,
  "product": "vessel-motion-p4",
  "architecture": "esp32p4",
  "version": "x.y.z",
  "size": 123,
  "sha256": "...",
  "url": "https://raw.githubusercontent.com/barba-productions/vessel-motion-p4-OTA/main/stable/vessel_motion_p4.bin"
}
```

## Publishing a release

Run from the main project workspace:

```
powershell -NoProfile -ExecutionPolicy Bypass -File release_ota.ps1 -Version x.y.z
```

The script bumps the version in `CMakeLists.txt`, builds, copies the binary
here, regenerates the manifest, commits and pushes this repo.
Web dashboard assets are not part of OTA — they are staged over HTTP by
`upload_web.ps1` (the fire-button post-flash task runs it automatically).
