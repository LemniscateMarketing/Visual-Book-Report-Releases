# Visual Book Report Releases

Official public release artifacts for the Visual Book Report desktop application.

This repository intentionally contains **release artifacts only**. The application source, private documentation, credentials, client reports, and internal configuration are not published here.

## Current stable tester release

The latest stable tester release is [Visual Book Report Desktop 0.1.23](../../releases/tag/desktop-v0.1.23):

- Product Release 0.3 (shown in the app as VBR Release 0.3)
- Report Core 0.4.8
- Desktop App 0.1.23
- MCP Tools / Claude Desktop MCPB 0.4.11
- Codex Plugin 0.4.1 (source-only; not a public release asset)

There is one Visual Book Report app for existing users, new testers, and friends. The Sharing Kit is only a convenience ZIP containing the same audited DMG and MCPB with checksums and instructions; it is not a separate edition.

Desktop 0.1.23 is a focused authoring-comfort and geometry-stability release.
The contextual **Add block** picker now contains its own layout and paint,
ignores catalog scrolling when deciding whether to reposition, and follows
settled reader-view transforms. This prevents the intermittent WebKit geometry
escape that could pull the picker and nearby authoring content toward the left.

Inline text editing now keeps selection feedback away from the words with a
soft offset outline and no active-typing shadow. The selected-block toolbar
uses a restrained near-content shadow instead of panel-sized depth, leaving
the text visually clear while the editing controls remain easy to find.

The lifecycle, persistence, cancellation, teardown, and export hardening from
Desktop 0.1.22 remains in place.

The compact **Theme & Brand Studio**, presentation-first **Project** tab, and
progressive **History & recovery** workflow introduced in Desktop 0.1.21 remain
unchanged in this release.

The desktop app continues to bundle the local VBR MCP server and runtime for
the in-app Codex flow. MCPB 0.4.11 carries the matching governed authoring and
lifecycle contracts for Claude Desktop; Claude still owns review, workspace
selection, and final installation approval.

The release was built from exact private source commit
`449c463208ea6009c43c9aae62c7e6288f16e078`. The private source and source-only
Codex Plugin are not included in this artifact-only repository.

The signed updater path was exercised in an isolated copy of Desktop 0.1.22.
That same app bundle advanced to 0.1.23, matched the complete candidate bundle,
and preserved the seeded project, device settings, and portable asset bytes.

## Install on Apple silicon macOS

1. Download `visual-book-report-desktop-0.1.23-darwin-arm64.dmg` from the [latest release](../../releases/latest).
2. Open the DMG and drag **Visual Book Report** into **Applications**.
3. This trusted-tester build is not yet Apple Developer ID signed or notarized. If macOS blocks the first launch, use the explicit **Open Anyway** control in **System Settings → Privacy & Security** after confirming that the download came from this repository.

The DMG includes a reversible uninstaller. Project data is preserved by default unless the tester explicitly selects the purge-data option.

## Update channel

Desktop releases use `desktop-v<major>.<minor>.<patch>` tags. Version `0.1.5` is the one-time manual bootstrap that installs the updater-capable application and its public verification key. From that build onward, the app checks this channel, offers **Install update & restart** for a newer compatible stable release, downloads the complete application archive, verifies its updater signature, replaces the installed app, and restarts it. **View release** remains available as a fallback.

The complete 0.1.23 release contains exactly seven public downloads for the
same app and version:

- `visual-book-report-desktop-0.1.23-darwin-arm64.dmg`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz.sig`
- `latest.json`
- `DESKTOP-RELEASE.json`
- `visual-book-report-0.4.11.mcpb`
- `Visual-Book-Report-0.1.23-Apple-Silicon-Sharing-Kit.zip`

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

Version 0.1.23 is Apple silicon (arm64) only and requires macOS 12 or newer. It
is an ad-hoc-signed, non-notarized tester build rather than a trusted
public-production installer. The optional MCPB is an unsigned custom tester
extension that still requires Claude Desktop review and approval. Confirm the
repository and release checksums before using Gatekeeper's explicit approval
path.
