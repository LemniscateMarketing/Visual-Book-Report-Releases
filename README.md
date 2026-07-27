# Visual Book Report Releases

Official public release artifacts for the Visual Book Report desktop application.

This repository intentionally contains **release artifacts only**. The application source, private documentation, credentials, client reports, and internal configuration are not published here.

## Install on Apple silicon macOS

1. Download the latest `Visual Book Report_<version>_aarch64.dmg` from [Releases](../../releases/latest).
2. Open the DMG and drag **Visual Book Report** into **Applications**.
3. Until the application is Developer ID signed and notarized, trusted testers must run:

   ```sh
   xattr -dr com.apple.quarantine "/Applications/Visual Book Report.app"
   open -a "Visual Book Report"
   ```

The DMG includes a reversible uninstaller. Project data is preserved by default unless the tester explicitly selects the purge-data option.

## Update channel

Desktop releases use `desktop-v<major>.<minor>.<patch>` tags. The installed application checks this release channel when it starts. When a newer stable desktop release is available, the app shows an **Open Release** notice; replacement remains manual while packages are unsigned.

Each release includes `DESKTOP-RELEASE.json` with the source commit, architecture, byte sizes, and SHA-256 hashes for verification.
