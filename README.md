# Visual Book Report Releases

Official public release artifacts for the Visual Book Report desktop application.

This repository intentionally contains **release artifacts only**. The application source, private documentation, credentials, client reports, and internal configuration are not published here.

## Current stable tester release

The latest stable tester release is [Visual Book Report Desktop 0.1.12](../../releases/tag/desktop-v0.1.12):

- VBR Release 0.1
- Report core 0.4.1
- Desktop app 0.1.12
- MCP tools / Claude Desktop MCPB 0.4.2

There is one Visual Book Report app for existing users, new testers, and friends. The Sharing Kit is only a convenience ZIP containing the same audited DMG and MCPB with checksums and instructions; it is not a separate edition.

## Install on Apple silicon macOS

1. Download `visual-book-report-desktop-0.1.12-darwin-arm64.dmg` from the [latest release](../../releases/latest).
2. Open the DMG and drag **Visual Book Report** into **Applications**.
3. This trusted-tester build is not yet Apple Developer ID signed or notarized. If macOS blocks the first launch, use the explicit **Open Anyway** control in **System Settings → Privacy & Security** after confirming that the download came from this repository.

The DMG includes a reversible uninstaller. Project data is preserved by default unless the tester explicitly selects the purge-data option.

## Update channel

Desktop releases use `desktop-v<major>.<minor>.<patch>` tags. Version `0.1.5` is the one-time manual bootstrap that installs the updater-capable application and its public verification key. From that build onward, the app checks this channel, offers **Install update & restart** for a newer compatible stable release, downloads the complete application archive, verifies its updater signature, replaces the installed app, and restarts it. **View release** remains available as a fallback.

The complete 0.1.12 release contains exactly seven public downloads for the
same app and version:

- `visual-book-report-desktop-0.1.12-darwin-arm64.dmg`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz.sig`
- `latest.json`
- `DESKTOP-RELEASE.json`
- `visual-book-report-0.4.2.mcpb`
- `Visual-Book-Report-0.1.12-Apple-Silicon-Sharing-Kit.zip`

The first five files are the canonical desktop/updater contract. The MCPB is
the optional Claude Desktop extension. The Sharing Kit contains the
byte-identical canonical DMG and MCPB plus checksums and tester instructions.
Neither companion download creates a second desktop-app edition.

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

For Claude Desktop, the preferred route is **Visual Book Report → Settings →
Integrations → Install in Claude Desktop…**. Visual Book Report verifies the
exact bundled MCPB and opens it with the registered Claude Desktop app. Claude
owns the extension review, workspace selection, and final installation
approval. The handoff does not mean the extension is installed or connected,
and Visual Book Report does not silently change Claude configuration.

If the in-app handoff is unavailable, download `visual-book-report-0.4.2.mcpb`
from the latest release and, in Claude Desktop, use **Settings → Extensions →
Advanced settings → Extension Developer → Install Extension**. Choose an
explicit workspace and enable persistence only if books should survive
restarts. Claude Desktop supplies Node, so no Node, npm, source checkout, or
Terminal setup is required. Visual Book Report app updates do not update the
Claude extension: each newer MCPB requires another VBR handoff or manual
selection, followed by Claude review and approval. Organization policy may
restrict custom extensions, and this MCPB is an unsigned tester extension.

To move a Codex- or Claude-created book into the desktop Project Library, use
`export_report_project` with profile `project-transfer`, save the exact JSON,
then choose **Library → Import** in Visual Book Report. The transfer is explicit
and user-controlled; automatic live mirroring is not implemented.

The lowercase ASCII filenames are part of the updater protocol. `latest.json` points to the archive under the same immutable desktop tag, and `DESKTOP-RELEASE.json` records the source commit, target, byte sizes, and SHA-256 hashes. A release is not activated until the uploaded asset names and bytes are read back and verified.

The updater signature protects the downloaded application archive. It does not replace Apple Developer ID signing or notarization, which remain required before ordinary public distribution without the trusted-tester warning above.

Version 0.1.12 is Apple silicon (arm64) only and requires macOS 12 or newer. It
is an ad-hoc-signed, non-notarized tester build rather than a trusted
public-production installer. Confirm the repository and release checksums
before using Gatekeeper's explicit approval path.
