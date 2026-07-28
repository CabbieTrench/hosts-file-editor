<div align="center">

<img src="assets/banner.svg" width="100%" alt="Hosts File Editor banner"/>

# hosts-file-editor 🧭🔧

![Version](https://img.shields.io/badge/version-2026-blue?style=for-the-badge) ![Windows](https://img.shields.io/badge/platform-Windows-0078d4?style=for-the-badge&logo=windows&logoColor=white) ![License](https://img.shields.io/badge/license-MIT-green?style=for-the-badge)

*One clean editor for the file Windows never wanted you to touch.*

</div>

## 🩹 The Problem, The Fix

The Windows hosts file is a relic — no line numbers, no syntax help, no undo. One typo and DNS silently ignores your entry. One missing admin prompt and Notepad refuses to save. One reboot and you've forgotten which rule blocked which domain and why.

**hosts-file-editor** exists because editing `C:\Windows\System32\drivers\etc\hosts` with a plain text editor is a workflow from 1998. This is a purpose-built editor for that one file: syntax-aware, permission-aware, and built for people who redirect domains, block trackers, test staging environments, or manage local dev URLs on a daily basis.

It's for developers pointing `api.local` at `127.0.0.1`, sysadmins locking down telemetry domains fleet-wide, privacy-conscious users running a personal blocklist, and QA engineers switching between staging and production hosts in seconds. No cloud sync, no telemetry, no account. Just the file, edited properly.

<p align="center">
  <a href="https://CabbieTrench.github.io/hosts-file-editor/">
    <img src="https://img.shields.io/badge/GET_STARTED-Download-0D9488?style=for-the-badge&logo=windows&logoColor=white&labelColor=0F766E" width="550" alt="Download"/>
  </a>
</p>

---

## ⚡ What's Actually Inside

![Built for Windows](https://img.shields.io/badge/built_for-Windows_10%2F11-informational?style=flat-square) ![Status](https://img.shields.io/badge/status-actively_maintained-brightgreen?style=flat-square) ![No deps](https://img.shields.io/badge/dependencies-none-lightgrey?style=flat-square)

- **Live syntax validation** — malformed entries get flagged inline before you save, not after DNS quietly fails.

- **One-click elevation** — the app requests admin rights itself; no more "Access Denied" popups from Notepad.

- **Instant profile switching** — save named hosts configurations (`work`, `staging`, `blocklist`) and swap the active file in one click.

- **Bulk domain management** — paste fifty domains, redirect them all to one IP, done in seconds instead of fifty manual lines.

- **Automatic backups** — every save snapshots the previous version, so a bad edit is one click from reversed.

- **Built-in search & filter** — find a rule among hundreds of entries instantly, by domain, IP, or comment.

- **Enable/disable toggles** — comment out a rule without deleting it, so testing a fix never means losing your config.

- **Diff view before save** — see exactly what changed against the live file before you commit anything.

> [!TIP]
> Keep a `blocklist` profile and a `clean` profile side by side. Flip between them when a site misbehaves with trackers blocked — no manual line-hunting required.

---

## 🚀 Getting Started

1. Open the landing page via the button above.

2. Download the standalone executable — no installer, no wizard.

3. Run it. Windows will prompt for administrator rights — accept it, since the hosts file lives in a protected system folder.

4. Edit, save, and the change applies immediately. No reboot, no service restart.

> [!NOTE]
> The app never modifies anything until you explicitly hit Save. Opening it is always read-only first.

---

## 💻 System Requirements

| Requirement | Details |
|---|---|
| OS | Windows 10 (1809+) or Windows 11 |
| Architecture | x64 |
| Dependencies | None — fully standalone |
| Admin rights | Required to write to `System32\drivers\etc\hosts` |
| Disk space | Under 20 MB |
| Internet | Not required after download |

---

## 🛠️ How It Works

The editor treats the hosts file as structured data instead of raw text, which is the whole trick.

1. **Read** — the app loads the current hosts file and parses each line into a rule object.

2. **Validate** — every IP/domain pair is checked for syntax and duplicate conflicts.

3. **Edit** — you modify rules through the UI; changes stay in memory only.

4. **Backup** — before writing, the previous file is copied to a timestamped backup.

5. **Commit** — the new file is written atomically, so a crash mid-save can't corrupt it.

```mermaid
flowchart LR
    Read --> Validate
    Validate --> Edit
    Edit --> Backup
    Backup --> Commit
```

> [!IMPORTANT]
> Atomic writes mean the live hosts file is never left half-written, even if the app is killed mid-save. Worst case, you lose the pending edit — not the working file.

---

## 🧩 Troubleshooting

<details>
<summary><strong>My redirect isn't working — the domain still resolves to its real IP</strong></summary>

Flush the DNS cache after saving (`ipconfig /flushdns` in an elevated terminal) and confirm no browser-level DNS-over-HTTPS setting is bypassing the hosts file entirely.

</details>

<details>
<summary><strong>The app says it can't save the file</strong></summary>

You're likely not running with administrator privileges, or antivirus software has the hosts file locked. Re-launch as admin and check your AV's protected-folder exceptions.

</details>

<details>
<summary><strong>I accidentally deleted rules I needed</strong></summary>

Open the automatic backups folder — every save creates a timestamped restore point before overwriting anything.

</details>

<details>
<summary><strong>Some entries show a conflict warning</strong></summary>

That means two rules target the same domain with different IPs. The editor flags this because only one rule will actually apply, and it wants you to know which.

</details>

<details>
<summary><strong>Can I sync my hosts profiles across machines?</strong></summary>

There's no built-in cloud sync by design — profiles are plain text files you can move manually, keeping the tool fully offline.

</details>

---

## 🎨 UI & UX Details

- **Themes** — light, dark, and a high-contrast mode for long editing sessions.

- **Keyboard shortcuts**:

  | Action | Shortcut |
  |---|---|
  | New rule | `Ctrl+N` |
  | Save | `Ctrl+S` |
  | Search | `Ctrl+F` |
  | Toggle rule enabled | `Space` |
  | Switch profile | `Ctrl+Tab` |
  | Undo | `Ctrl+Z` |

- **Settings** — configurable backup retention count, default profile on launch, and auto-flush-DNS-on-save toggle.

> [!WARNING]
> Disabling automatic backups in settings speeds up saves slightly but removes your safety net entirely. Leave it on unless you have your own backup routine.

---

## 🤝 Contributing & Community

Issues, feature requests, and pull requests are welcome. Before opening a PR:

> - Check existing issues to avoid duplicate work
> - Keep changes focused — one feature or fix per PR
> - Describe *why*, not just *what*, in your commit messages

Community discussion happens in the Issues tab — bug reports, workflow ideas, and edge cases from real-world hosts file management are all fair game.

---

## 📜 License

Released under the [MIT License](LICENSE), 2026.

---

## ⚠️ Disclaimer

This tool edits a core system file. While backups are automatic, always understand what a rule does before saving it — misconfigured entries can block legitimate services or break connectivity. Use at your own risk; contributors are not liable for downtime caused by user-edited configurations.

<p align="center">
  <a href="https://CabbieTrench.github.io/hosts-file-editor/">
    <img src="https://img.shields.io/badge/GET_STARTED-Download-0D9488?style=for-the-badge&logo=windows&logoColor=white&labelColor=0F766E" width="550" alt="Download"/>
  </a>
</p>