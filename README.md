# Visual Book Report Releases

Official public release artifacts for the Visual Book Report desktop application.

This repository intentionally contains **release artifacts only**. The application source, private documentation, credentials, client reports, and internal configuration are not published here.

## Current stable tester release

The latest stable tester release is [Visual Book Report Desktop 0.1.24](../../releases/tag/desktop-v0.1.24):

- Product Release 0.4 (shown in the app as VBR Release 0.4)
- Report Core 0.4.8
- Desktop App 0.1.24
- MCP Tools / Claude Desktop MCPB 0.4.11
- Codex Plugin 0.4.1 (source-only; not a public release asset)

There is one Visual Book Report app for existing users, new testers, and friends. The Sharing Kit is only a convenience ZIP containing the same audited DMG and MCPB with checksums and instructions; it is not a separate edition.

Desktop 0.1.24 advances the compatibility line to **VBR Release 0.4** and makes
the Claude Desktop extension update state explicit. Settings now distinguishes
the installed and bundled MCPB versions, reports whether the installed
extension is enabled, and labels missing, older, current, newer, or unknown
states without inferring installation from the handoff itself.

When an older extension is installed, Settings offers **Update in Claude
Desktop…**. Visual Book Report verifies the exact bundled MCPB before opening
it, while Claude continues to own review, workspace selection, and final
approval. A newer installed extension is protected from downgrade, and
unreadable or inconsistent local evidence fails closed rather than claiming a
safe update.

The authoring-comfort, lifecycle, persistence, cancellation, teardown, export,
Theme & Brand Studio, Project, and History & recovery work from the preceding
stable releases remains in place.

The desktop app continues to bundle the local VBR MCP server and Node runtime
for the in-app Codex flow. MCPB 0.4.11 carries the matching governed authoring
and lifecycle contracts for Claude Desktop.

The release was built from exact private source commit
`57e0a07b1805ff778b922574a316cc30f8edffef`. The private source and source-only
Codex Plugin are not included in this artifact-only repository.

The exact packaged app passed strict signature, updater-metadata, artifact-hash,
and rendered Settings checks. In the live Settings smoke it truthfully reported
an enabled installed MCPB 0.4.9, bundled MCPB 0.4.11, and **Update available**
without modifying Claude or claiming that approval had occurred.

## Install on Apple silicon macOS

1. Download `visual-book-report-desktop-0.1.24-darwin-arm64.dmg` from the [latest release](../../releases/latest).
2. Open the DMG and drag **Visual Book Report** into **Applications**.
3. This trusted-tester build is not yet Apple Developer ID signed or notarized. If macOS blocks the first launch, use the explicit **Open Anyway** control in **System Settings → Privacy & Security** after confirming that the download came from this repository.

The DMG includes a reversible uninstaller. Project data is preserved by default unless the tester explicitly selects the purge-data option.

## Update channel

Desktop releases use `desktop-v<major>.<minor>.<patch>` tags. Version `0.1.5` is the one-time manual bootstrap that installs the updater-capable application and its public verification key. From that build onward, the app checks this channel, offers **Install update & restart** for a newer compatible stable release, downloads the complete application archive, verifies its updater signature, replaces the installed app, and restarts it. **View release** remains available as a fallback.

The complete 0.1.24 release contains exactly seven public downloads for the
same app and version:

- `visual-book-report-desktop-0.1.24-darwin-arm64.dmg`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz.sig`
- `latest.json`
- `DESKTOP-RELEASE.json`
- `visual-book-report-0.4.11.mcpb`
- `Visual-Book-Report-0.1.24-Apple-Silicon-Sharing-Kit.zip`

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

For Claude Desktop, open **Visual Book Report → Settings → Integrations**. The
Claude card compares the installed extension with the exact bundled MCPB and
shows **Install in Claude Desktop…** or **Update in Claude Desktop…** when an
approval handoff is appropriate. Visual Book Report verifies the bundled file
and opens it with the registered Claude Desktop app. Claude owns extension
review, workspace selection, and final approval. Opening the handoff does not
mean the extension was installed or connected, and Visual Book Report never
silently changes Claude configuration.

If the in-app handoff is unavailable, download `visual-book-report-0.4.11.mcpb`
from the latest release and, in Claude Desktop, use **Settings → Extensions →
Advanced settings → Extension Developer → Install Extension**. Choose an
explicit workspace and enable persistence only if books should survive
restarts. Claude Desktop supplies Node, so no Node, npm, source checkout, or
Terminal setup is required. Visual Book Report app updates do not update the
Claude extension: each newer MCPB requires another VBR handoff or manual
selection, followed by Claude review and approval. Organization policy may
restrict custom extensions, and this MCPB is an unsigned tester extension.

**Library → Import** provides one guarded drop-or-choose surface for an
ordinary VBR project JSON file, a digest-verified `project-transfer` JSON file,
or a standalone VBR `.html`/`.htm` export. To move a Codex- or Claude-created
book into the desktop Project Library, use `export_report_project` with profile
`project-transfer`, save the exact JSON, then import it there. Supported project
dependency metadata is preserved, and collision-safe project and report IDs
keep the imported book separate from existing Library content.

Standalone VBR HTML is read only as text. The app validates its embedded
package and report data and never executes, injects, or iframes the file. The
result is a new editable recovery project; version history, checkpoints, and
private notes are not restored. Unsupported extensions or invalid data produce
an inline error, add nothing to the Library, and keep the transfer explicit and
user-controlled. Automatic live mirroring is not implemented.

The lowercase ASCII filenames are part of the updater protocol. `latest.json` points to the archive under the same immutable desktop tag, and `DESKTOP-RELEASE.json` records the source commit, target, byte sizes, and SHA-256 hashes. A release is not activated until the uploaded asset names and bytes are read back and verified.

The updater signature protects the downloaded application archive. It does not replace Apple Developer ID signing or notarization, which remain required before ordinary public distribution without the trusted-tester warning above.

Version 0.1.24 is Apple silicon (arm64) only and requires macOS 12 or newer. It
is an ad-hoc-signed, non-notarized tester build rather than a trusted
public-production installer. The optional MCPB is an unsigned custom tester
extension that still requires Claude Desktop review and approval. Confirm the
repository and release checksums before using Gatekeeper's explicit approval
path.
