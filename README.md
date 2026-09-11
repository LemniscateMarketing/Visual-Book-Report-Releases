# Visual Book Report Releases

Official public release artifacts only. Private source, internal documents,
client reports and credentials do not belong in this repository.

## Current stable tester: Desktop 0.1.29

[Desktop 0.1.29](../../releases/tag/desktop-v0.1.29) is published stable/latest.
All seven draft and fresh anonymous public downloads match their audited hashes.
Use the [latest published release](../../releases/latest) for downloads.

Apple-silicon macOS 12+ stable tester. This is an HTML export reliability repair,
not a new feature phase or a change to the Product Release line.

| Coordinate | Version |
| --- | --- |
| Product Release | 0.4 |
| Report Core | 0.4.10, unchanged |
| Desktop App | 0.1.29 |
| MCP Tools / Claude Desktop MCPB | 0.4.13, unchanged |
| Codex Plugin | 0.4.1, unchanged/source-only; not a release asset |

## Repair

Overlapping HTML exports now return an explicit busy result before editor
synchronization or injected hooks. One active export retains its own download,
status and controls until it settles. Retry, callback chaining, failure and
teardown behavior have regression coverage. No request is silently queued or
reported as another report's successful download.

This addresses a confirmed integration/API race; ordinary double-click
reachability through a disabled menu was not established. Existing validation,
asset restrictions, Offline/Connected profiles, toolbar placement and visual
styling remain unchanged. Previous keyboard-focus, nested-editing, updater,
recovery and local integration repairs remain included.

## Updating

Desktop 0.1.25 through 0.1.28 users in writable application locations can use
**Settings → App & Updates → Check now → Install update & restart** once this
release is activated. The whole app updates together. The official feed,
verification key and app identifier are unchanged.

For 0.1.24 and earlier, retain the old app and use the verified DMG for this
first upgrade. This conservative guidance does not mean all earlier updates
failed. New/manual installations follow the DMG guide into your own
Home/Applications folder. Do not uninstall, delete books or merge app bundles.
Protected/read-only locations may require manual placement. Do not remove
quarantine attributes or disable Gatekeeper. For this non-notarized tester,
use macOS's explicit **Open Anyway** approval only after verifying the source
repository and release checksums.

VBR updates do not silently update Claude's installed extension or rewrite
Codex/Claude client configuration. Exact MCPB 0.4.13 installations need no new
extension version for this Desktop-only repair. Older Claude extensions use
VBR's verified update handoff and Claude's separate review/workspace approval.
The Codex Plugin remains source-only; automatic project mirroring is not implemented.

## Verification and limits

Exact build source: `3a4abb85abc390e9b21168210005b1d8ea76453e`.
The candidate passed 538 source commands, 76 native host tests, 21 installer
tests, all three network-policy tests and 46 updater compatibility cases.
Independent static, app, updater, mounted-DMG and Sharing Kit audits passed.
The updater signature verifies and altered bytes are rejected; every app file
and permission matches the updater archive and mounted DMG. MCPB 0.4.13 is
byte-identical to the previously published installer.

Isolated browser checks reached completed Offline and Connected export status,
re-enabled controls and normal navigation. The browser download observer timed
out, so that UI observation is not claimed as a new saved-file identity.
Source/package tests provide separate artifact evidence. No new visual design
or fresh Claude Design approval is claimed.

All seven draft downloads and fresh anonymous public downloads passed exact
name, length and SHA-256 checks, including a separate independent readback.
The actual backed-up 0.1.28-to-0.1.29 installed update is being verified
separately; no completed transition is claimed at this checkpoint. Earlier
normal updater transitions through 0.1.28 remain separate historical proof.

This remains an ad-hoc-signed, non-notarized tester app with an unsigned MCPB,
not an Apple Developer-ID/notarized production-public installer. No universal
future-update, power-loss recovery, post-launch health rollback, all-Mac/all-book
or complete cross-client certification is claimed. Publisher/license decisions
remain separate. No fresh packaged-MCP session or client installation is claimed.

## Downloads

Exactly seven intended public assets:

- `visual-book-report-desktop-0.1.29-darwin-arm64.dmg`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz`
- `visual-book-report-desktop-darwin-aarch64.app.tar.gz.sig`
- `latest.json`
- `DESKTOP-RELEASE.json`
- `visual-book-report-0.4.13.mcpb`
- `Visual-Book-Report-0.1.29-Apple-Silicon-Sharing-Kit.zip`

The Sharing Kit wraps the same audited DMG and MCPB with checksums and
instructions; it is not another app edition. The app already includes the
local MCP server and Node runtime for its Codex flow. `DESKTOP-RELEASE.json`
records hashes, while `latest.json` points to the signed archive under the
same immutable tag. Private source/docs, user data, credentials, the internal
static ZIP and source-only Codex Plugin are not uploaded here.

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

If the in-app handoff is unavailable, download `visual-book-report-0.4.13.mcpb`
from the latest release and, in Claude Desktop, use **Settings → Extensions →
Advanced settings → Extension Developer → Install Extension**. Choose an
explicit workspace and enable persistence only if books should survive
restarts. Claude Desktop supplies Node, so no Node, npm, source checkout, or
Terminal setup is required. Visual Book Report app updates do not update the
Claude extension: each newer MCPB requires another VBR handoff or manual
selection, followed by Claude review and approval. Organization policy may
restrict custom extensions, and this MCPB is an unsigned tester extension.
An existing exact MCPB 0.4.13 installation does not need a new extension version
for this Desktop-only repair.

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

Version 0.1.29 is Apple silicon (arm64) only and requires macOS 12 or newer. It
is an ad-hoc-signed, non-notarized tester build rather than a trusted
public-production installer. The optional MCPB is an unsigned custom tester
extension that still requires Claude Desktop review and approval. Confirm the
repository and release checksums before using Gatekeeper's explicit approval
path.
