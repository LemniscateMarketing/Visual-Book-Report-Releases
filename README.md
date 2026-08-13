# Visual Book Report Releases

Official public release artifacts for the Visual Book Report desktop application.

This repository intentionally contains **release artifacts only**. The application source, private documentation, credentials, client reports, and internal configuration are not published here.

## Install on Apple silicon macOS

1. Download the latest `visual-book-report-desktop-<version>-darwin-arm64.dmg` from [Releases](../../releases/latest).
2. Open the DMG and drag **Visual Book Report** into **Applications**.
3. This trusted-tester build is not yet Apple Developer ID signed or notarized. If macOS blocks the first launch, use the explicit **Open Anyway** control in **System Settings → Privacy & Security** after confirming that the download came from this repository.

The DMG includes a reversible uninstaller. Project data is preserved by default unless the tester explicitly selects the purge-data option.

## Update channel

Desktop releases use `desktop-v<major>.<minor>.<patch>` tags. Version `0.1.5` is the one-time manual bootstrap that installs the updater-capable application and its public verification key. From that build onward, the app checks this channel, offers **Install update & restart** for a newer compatible stable release, downloads the complete application archive, verifies its updater signature, replaces the installed app, and restarts it. **View release** remains available as a fallback.

Each complete Apple-silicon desktop release contains these five required
canonical desktop/updater artifacts:

- `visual-book-report-desktop-<version>-darwin-arm64.dmg`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz.sig`
- `latest.json`
- `DESKTOP-RELEASE.json`

A release may also include optional companion downloads for that same app and
version:

- `Visual-Book-Report-<version>-Apple-Silicon-Sharing-Kit.zip` contains the
  byte-identical canonical DMG, instructions, checksums, and the optional
  Claude Desktop extension.
- `visual-book-report-<mcp-version>.mcpb` installs the governed VBR tools
  in Claude Desktop without creating a separate desktop-app edition.

The desktop app already bundles the local VBR MCP server and Node runtime for
the in-app Codex connection flow. Companion assets do not change updater
selection: the app accepts only the exact canonical metadata, archive, and
signature filenames for its architecture.

## Use the AI integrations

For Codex, open **Visual Book Report → Settings → Integrations → Codex**,
choose the intended workspace behavior, then select **Connect** and **Verify**.
The app supplies the VBR MCP runtime and Node sidecar. Current builds can use a
supported standalone Codex CLI or the Codex CLI bundled by ChatGPT Desktop; a
separate system Node installation is not required.

For Claude Desktop, download the `visual-book-report-<mcp-version>.mcpb`
companion from the latest release. In Claude Desktop, use **Settings →
Extensions → Advanced settings → Extension Developer → Install Extension**,
choose an explicit workspace, and enable persistence if books should survive
restarts. Claude Desktop supplies Node, so no Node, npm, source checkout, or
Terminal setup is required. Custom MCPB installation and updates are manual,
and organization policy may restrict custom extensions. The MCPB is currently
an unsigned tester extension.

To move a Codex- or Claude-created book into the desktop Project Library, use
`export_report_project` with profile `project-transfer`, save the exact JSON,
then choose **Library → Import** in Visual Book Report. The transfer is explicit
and user-controlled; automatic live mirroring is not implemented.

The lowercase ASCII filenames are part of the updater protocol. `latest.json` points to the archive under the same immutable desktop tag, and `DESKTOP-RELEASE.json` records the source commit, target, byte sizes, and SHA-256 hashes. A release is not activated until the uploaded asset names and bytes are read back and verified.

The updater signature protects the downloaded application archive. It does not replace Apple Developer ID signing or notarization, which remain required before ordinary public distribution without the trusted-tester warning above.
