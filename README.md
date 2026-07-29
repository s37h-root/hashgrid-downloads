# HashGrid Bridge — downloads

Public download host for **HashGrid Bridge**. This repo contains **no source
code** — only released binaries, published automatically by CI from the private
build repos.

The bridge runs on a machine inside your home network and lets the HashGrid iOS
app monitor and control your miners from anywhere.

---

## Download

| Platform | File |
|---|---|
| **macOS** (menu-bar app, macOS 14.0+) | [HashGrid-Bridge-macOS.dmg](https://github.com/s37h-root/hashgrid-downloads/releases/latest/download/HashGrid-Bridge-macOS.dmg) |
| **Windows** (tray app, Windows 10/11 64-bit) | [HashGrid-Bridge-Windows.zip](https://github.com/s37h-root/hashgrid-downloads/releases/latest/download/HashGrid-Bridge-Windows.zip) |
| **Umbrel** | Install from the Umbrel app store — see below |

Those two links always resolve to the newest release — the filenames never
change, so they are safe to link to permanently. Older versions stay available
under [Releases](https://github.com/s37h-root/hashgrid-downloads/releases); the
version is in the release title, and the app reports its own version once
installed.

---

## Installing

### macOS

The app is **not yet signed with an Apple Developer certificate**, so macOS will
refuse to open it on the first try. This is expected.

1. Open the `.dmg` and drag **HashGrid Bridge** to Applications.
2. **Right-click** the app in Applications and choose **Open**.
3. Click **Open** in the dialog.

You only need to do this once. Double-clicking the first time shows *"cannot be
opened because the developer cannot be verified"* — right-click → Open is the
supported way around it.

If macOS says the app is **damaged**, it was quarantined on download. Clear it:

```bash
xattr -dr com.apple.quarantine "/Applications/HashGrid Bridge.app"
```

### Windows

The executable is **not yet code-signed**, so SmartScreen will warn on first run.

1. Unzip anywhere.
2. Run `HashGridBridge.exe`.
3. On the blue SmartScreen dialog, click **More info** → **Run anyway**.

### Umbrel

Install **HashGrid Bridge** from the Umbrel app store. Nothing to download here —
Umbrel pulls the Docker image itself.

---

## Verifying a download

Each platform ships a checksum file alongside its binary —
`SHA256SUMS-macos.txt` and `SHA256SUMS-windows.txt`. Download the one matching
your platform into the same folder as the binary, then:

```bash
shasum -a 256 -c SHA256SUMS-macos.txt        # macOS
```

```powershell
# Windows — compare this against the hash in SHA256SUMS-windows.txt
Get-FileHash .\HashGrid-Bridge-Windows.zip -Algorithm SHA256
```

---

## Security

The bridge holds a persistent Ed25519 identity key and pins itself to your iOS
app on first pairing. When you pair, the app shows a **six-group fingerprint** —
**all six groups must match** what the bridge displays. If they don't, stop and
re-pair; a mismatch means you are not talking to your bridge.

The relay that carries traffic between the app and the bridge is untrusted by
design: it routes encrypted payloads and never originates commands.

---

## Issues

Report problems at [hashgrid-umbrel/issues](https://github.com/s37h-root/hashgrid-umbrel/issues).
