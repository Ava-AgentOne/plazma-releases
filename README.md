<p align="center">
  <img src="icon.png" width="128" height="128" alt="The PLAzma mascot">
</p>

<h1 align="center">PLAzma handheld firmware</h1>

Firmware releases for the **PLAzma** handheld, an ESP32-S3 device with a 3.5" touch
screen. The handheld downloads these over Wi-Fi by itself, so nothing here needs to be
installed by hand. This repo holds only the releases, which lets the device fetch them
without a password.

## How the handheld updates

1. Once it is on Wi-Fi after starting up, it reads `firmware.json` from the
   **[latest release](https://github.com/Ava-AgentOne/plazma-releases/releases/latest)**.
2. **It checks the signature** (`firmware.json.sig`) against the key built into it, and
   ignores anything that is not signed with the project's key.
3. If that version is newer than the one it is running, **Settings → Firmware** says
   *update ready*. Nothing installs until you tap **Install**.
4. It downloads the image into its spare slot and checks it against the size and SHA-256
   named in the signed `firmware.json`, then restarts into it. If the new version does not
   start properly, the handheld goes back to the previous one by itself.

New versions go out as a **pre-release** first, for testing. The handheld only reads the
latest full release, so it is not offered a test version until it is promoted.

## What each release holds

| file | what it is |
|---|---|
| `plazma-handheld-<version>.bin` | the firmware image |
| `firmware.json` | product, version, file name, size, SHA-256, build date, commit, a one-line summary |
| `firmware.json.sig` | ECDSA P-256 signature over `firmware.json` |

The filament data is updated separately, from
[plazma-library](https://github.com/Ava-AgentOne/plazma-library).
