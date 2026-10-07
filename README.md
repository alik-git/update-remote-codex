# Update Remote Codex

A portable agent skill for updating Codex on a remote host and verifying that it reconnects.

It handles the distinction between a desktop app, a separately installed CLI, and a managed app-server. It discovers the user's installation rather than assuming a particular machine, account, operating system, package manager, or release channel.

## Install

In Codex, ask:

```text
Use $skill-installer to install https://github.com/alik-git/update-remote-codex/tree/main/skills/update-remote-codex.
```

For another agent supporting the Agent Skills format, copy `skills/update-remote-codex` into that agent's supported skill directory. See its documentation for the correct location.

## Use

```text
Use $update-remote-codex to update Codex on my selected remote host and verify it reconnects.
```

The agent needs an existing trusted connection and authorization to perform the requested maintenance. If several hosts or installations are possible, name the intended one. No account connection, SSH configuration, credential, or executable updater is bundled with this repository.

## Design

The skill keeps discovery short, preserves channels and version pins, limits restarts to the intended processes, and verifies the running server separately from installed binaries. It treats unavailable GUI checks as incomplete evidence and reports partial updates honestly.

The workflow adapts to the target OS and installed command versions. Desktop updates apply only where a desktop app exists; a headless host can have only a CLI or server.

This is an independent community skill. Review [SKILL.md](skills/update-remote-codex/SKILL.md) before using it. Commands and updater behavior can change across Codex versions.

## Official references

- [Build skills](https://learn.chatgpt.com/docs/build-skills)
- [Remote connections](https://learn.chatgpt.com/docs/remote-connections)
- [Developer commands](https://learn.chatgpt.com/docs/developer-commands)
- [Homebrew and npm update examples](https://developers.openai.com/cookbook/examples/codex/using_goals_in_codex)

## License

[MIT](LICENSE).
