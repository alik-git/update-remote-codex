---
name: update-remote-codex
description: Update Codex on a user-selected remote host, distinguish desktop, CLI, and managed server installations, and verify reconnection. Use for remote Codex maintenance, not initial host setup or local-only updates.
---

# Update Remote Codex

Update the intended installation through its existing update mechanism, then verify the running service and the user's connection. A desktop app, a shell CLI, and a managed app-server can use different executables and versions.

## Establish the target and scope

Reuse the user's selected host, account, and trusted connection. Ask only if the target or requested scope is ambiguous. Work within existing update and interruption authorization; selecting this skill alone does not authorize changes. A version-check request stays read-only.

Preserve active work. An authorized update can include necessary restarts, but does not authorize stopping unrelated jobs. If a restart would interrupt work outside the authorized scope, finish independent preparation before asking about that interruption. Do not promise interrupted chats will resume automatically.

Use an independent management connection when restarting Codex could sever the current one. Keep SSH host-key verification enabled. An unknown or changed host key needs trusted verification before proceeding; do not silently accept it. Do not copy credentials, inspect authentication files, dump environments, or print full process arguments.

## Inspect once

Batch read-only checks and record only what helps choose the update path:

- Resolve `codex` and its version in the remote user's **login shell**. A bare SSH command can have a different `PATH`; use the host's actual shell and OS, not an assumed shell or home directory.
- Identify the existing package manager, release channel, and deliberate version pins.
- If a desktop app exists and is in scope, locate its installed bundle and version. Do not assume its name, path, or bundled CLI matches the shell CLI.
- Identify the relevant running server and its executable. Prefer a managed version/status command; limit process inspection to PID, executable path, and start time.

When supported, `codex app-server daemon version` distinguishes the calling CLI, managed package, and live server. Check installed `--help` before using unfamiliar daemon commands. A missing daemon is not permission to bootstrap one.

## Apply the appropriate update

Preserve the installation's channel and deliberate pins. Do not downgrade a newer or prerelease server just to match a stable CLI. If the update mechanism cannot establish its target version/channel safely, resolve that uncertainty before mutation.

**CLI:** use the existing manager or supported self-update command. Examples for an established stable installation are `brew update` followed by `brew upgrade --cask codex`, or `npm install -g @openai/codex@latest`. Run them on the intended host and in the owning user's environment. Do not switch managers, perform an unrelated full-system upgrade, or add privilege escalation unnecessarily.

**Desktop:** prefer the app's native updater or its established distribution mechanism. Verify an app-update tool targets the remote host; some tools check only the controlling computer. A staged update may install on quit and relaunch. After applying it, check once more for a newer offered release; apply at most one additional staged release in this pass. If more remain, report that rather than looping indefinitely. Keep the installed release channel.

**Server:** replacing a CLI binary does not update an already-running process. Use its existing manager to update or restart only the relevant server when needed. Confirm the managed update's source and channel first. Do not use `--from-cli` merely to synchronize versions: it can replace and pin the managed package.

For a server you manage directly, retain its launch configuration and restart method. Do not create new public listeners or alter authentication, network policy, pairing, or remote-control permissions.

## Bound recovery

Try graceful quit or the service manager first. After a reasonable grace interval, a single targeted termination is appropriate only with interruption authorization and a freshly verified PID, executable, and start time. Avoid broad process kills and force-killing. If it still cannot stop or start, report the blocker instead of escalating automatically or rebooting the host.

After one remote GUI or permission failure, use available status checks. A locked desktop or unavailable update dialog is not evidence that the app is current. If the updater requires user interaction, report the remaining step; do not scrape application internals, substitute an unverified download, or disable signature checks to bypass it.

## Verify once and report

Open a fresh management connection. Recheck installed versions and the live server's response. Exercise the normal remote client path when accessible; a PID, cache, or installed binary alone does not prove client reconnection or model availability.

State which components changed, which were intentionally preserved, and whether normal reconnection was verified. Distinguish partial updates and remaining interaction from completion. Use local help and official documentation for unresolved behavior instead of repeated speculative probes.
