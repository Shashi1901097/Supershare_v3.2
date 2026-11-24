# Supershare_v3.2

Transfer data with secure and high speed with your family and friends.

Super Share is an Android app that sends files directly from phone to phone over Wi-Fi Direct. It needs no internet, no accounts and no servers.

## Features

- **One phone to one phone**: choose files, tap Send, scan the receiver's QR code, and sharing starts.
- **Group Share**: choose files, tap Send, show a QR code. Receivers scan it, their names appear in a list, and you tap Confirm to start sending to all of them.
- **Built-in file picker** with tabs for All Files, Videos, Apps, Photos and Audio. It has folders, albums, date-grouped photos, search, and a selected-file counter.
- **Cancel individual files** with the ✕ button, for both one phone and group. The receiver deletes the partial copy.
- **Resume**: an interrupted transfer continues where it stopped.
- **Storage check**: files that do not fit on the receiver are refused, and the receiver is told how much space is needed.
- **Fast**: encrypted parallel streams over Wi-Fi Direct (5 GHz when available).

## How to use

**Send to one phone**
1. Receiver: open **Receive**. A QR code appears.
2. Sender: tap **Send**, tick the files, tap **SEND**, and scan the receiver's QR code.

**Group Share**
1. Sender: tap **Group Share**, tick the files, tap **SEND**. A QR code appears.
2. Receivers: open **Receive**, tap **Scan QR**, and scan it. Each name appears in the sender's list.
3. Sender: tap **Confirm**. Files go to every receiver in the list.

Received files are saved in `Downloads/SuperShare` and shown under **My received files**.

## Security

- The pairing code is 8 random characters (letters, digits and special characters), new for every session. It is carried only in the QR code and never typed.
- The code is the password of an SRP-6a key exchange, not a key. A recorded conversation cannot be used to guess it offline, and the receiver locks out after 5 wrong attempts.
- All file names, sizes and data are encrypted and authenticated with AES-256-GCM.
- The peer's input is validated: file counts, sizes, names, connection limits.
- There are no accounts, ads, analytics or servers, and backups are disabled.

Details and test results are in `docs/SECURITY_AND_TESTING.md`.

## Requirements

- Android 10 (API 29) or newer
- A phone with Wi-Fi Direct
- Google Play services (for the QR scanner)

## Permissions

| Permission | Why |
|---|---|
| Nearby Wi-Fi devices / Location (older Android) | Create and join the Wi-Fi Direct group |
| Photos, videos and audio | Show them in the file picker |
| All files access | Documents, archives, big files and Internal Storage browsing |

## Build

```
git clone <your-repo-url>
cd SuperShare
./gradlew assembleDebug        # debug APK
./gradlew testDebugUnitTest    # automated tests
```

The `.github/workflows/build.yml` workflow builds the APK and publishes it to GitHub Releases on every push.

To sign a release, add these repository secrets: `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS` and `KEY_PASSWORD`. Run `release.yml` to build the Play Store bundle (AAB).

## Project layout

```
app/src/main/java/com/supershare/app/
  MainActivity.kt   app logic and state
  Screens.kt        Send, Group, Receive and Files screens
  Picker.kt         file picker (tabs, folders, thumbnails)
  Qr.kt             QR code drawing
  Ui.kt             theme and shared widgets
  core/             transfer engine in plain Java: Sender, Receiver, Keys, Srp, Crypto
docs/               security report, privacy policy, Play Store checklist
```

## Known limits

- Apps are shared as their base APK only, so apps installed as split bundles may not install on the receiver.
- The QR scanner needs Google Play services.
- Test on real phones before publishing. The transfer engine is tested on one computer, but Wi-Fi Direct behaviour differs between phone brands.

## License and author

© 2026 Shashikumar H G. All rights reserved.
