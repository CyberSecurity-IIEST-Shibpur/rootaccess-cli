# RootAccess CLI (`rootaccess`)

[![Release](https://img.shields.io/github/v/release/CyberSecurity-IIEST-Shibpur/rootaccess-cli?color=brightgreen&label=latest%20release)](https://github.com/CyberSecurity-IIEST-Shibpur/rootaccess-cli/releases)
[![Platform](https://img.shields.io/badge/platform-linux%20%7C%20macos%20%7C%20windows-blue)](#installation)
[![License](https://img.shields.io/github/license/CyberSecurity-IIEST-Shibpur/rootaccess-cli)](LICENSE)

The official command-line interface for the **[RootAccess](https://ctf.rootaccess.live)** CTF platform.

Manage your competition lifecycle directly from your terminal: browse challenges, submit flags, track the scoreboard, and author or host contests with direct file attachment uploads.

---

## Installation

### Quick Install (Linux & macOS)

Run the one-line installer script:

```bash
curl -s https://ctf.rootaccess.live/install.sh | bash
```

### Direct Binary Download

Pre-compiled binaries for each platform are available on the **[Releases Page](https://github.com/CyberSecurity-IIEST-Shibpur/rootaccess-cli/releases)**:

| Platform | Architecture | Binary |
|---|---|---|
| **Linux** | AMD64 (x86_64) | [`rootaccess-linux-amd64`](https://github.com/CyberSecurity-IIEST-Shibpur/rootaccess-cli/releases/latest/download/rootaccess-linux-amd64) |
| **Linux** | ARM64 (aarch64) | [`rootaccess-linux-arm64`](https://github.com/CyberSecurity-IIEST-Shibpur/rootaccess-cli/releases/latest/download/rootaccess-linux-arm64) |
| **macOS** | Apple Silicon (M1/M2/M3/M4) | [`rootaccess-darwin-arm64`](https://github.com/CyberSecurity-IIEST-Shibpur/rootaccess-cli/releases/latest/download/rootaccess-darwin-arm64) |
| **macOS** | Intel (x86_64) | [`rootaccess-darwin-amd64`](https://github.com/CyberSecurity-IIEST-Shibpur/rootaccess-cli/releases/latest/download/rootaccess-darwin-amd64) |
| **Windows** | AMD64 (x86_64) | [`rootaccess-windows-amd64.exe`](https://github.com/CyberSecurity-IIEST-Shibpur/rootaccess-cli/releases/latest/download/rootaccess-windows-amd64.exe) |

#### Linux / macOS Manual Setup

```bash
# Example for Linux AMD64
curl -L -o rootaccess https://github.com/CyberSecurity-IIEST-Shibpur/rootaccess-cli/releases/latest/download/rootaccess-linux-amd64
chmod +x rootaccess
sudo mv rootaccess /usr/local/bin/
```

Verify your installation:

```bash
rootaccess version
```

---

## Quickstart

### 1. Authenticate

```bash
rootaccess login
```

Opens your default web browser for OAuth login. Once authenticated, your session credentials are automatically saved to `~/.config/rootaccess/config.json`.

Confirm your logged-in profile:

```bash
rootaccess whoami
```

### 2. Contests & Challenges

Contests scope competition challenges. View running and upcoming contests and register your team:

```bash
rootaccess contests                          # List active & upcoming contests
rootaccess contests join <CONTEST_ID>        # Register your team for a contest
rootaccess contests leave <CONTEST_ID>       # Unregister
```

Browse challenges (defaults to the currently active contest):

```bash
rootaccess challenges                        # View challenges in active contest
rootaccess challenges --contest <ID>         # View challenges in a specific contest
```

Inspect details and submit flags:

```bash
rootaccess open <CHALLENGE_ID>               # View challenge description & file downloads
rootaccess submit <CHALLENGE_ID> <FLAG>      # Submit your flag (e.g. RootAccess{...})
rootaccess scoreboard                        # View real-time standings
```

---

## Contest Collaborator & Author Commands

For contest hosts and challenge creators:

### Authoring Questions & Uploading Attachments

Add questions/challenges with local file uploads and Markdown descriptions:

```bash
rootaccess collab challenge add <CONTEST_ID> \
  --title "Ghost Protocol" \
  --category rev \
  --difficulty hard \
  --points 500 \
  --min-points 100 \
  --decay 20 \
  --flag "RootAccess{packet_master_1337}" \
  --desc-file ./challenge/README.md \
  --file ./challenge/netrev.bin \
  --tags "rev,networking" \
  --hint "Inspect the custom TCP handshake:50" \
  --round <ROUND_ID>
```

> **Aliases:** `rootaccess question add` and `rootaccess challenges add` can also be used.

#### Direct Attachment Uploads

Upload standalone handout archives or files directly to contest cloud storage:

```bash
rootaccess collab challenge upload <CONTEST_ID> ./handout.tar.gz
```

#### List Contest Questions

```bash
rootaccess collab challenge list <CONTEST_ID>
```

### Contest Hosting Duties

```bash
rootaccess collab request                    # Submit a new contest hosting request
rootaccess collab requests                   # View status of hosting applications
rootaccess collab cancel <REQUEST_ID>        # Cancel a pending request
rootaccess collab contests                   # List contests you manage
rootaccess collab invite accept <TOKEN>      # Accept collaborator invite
```

---

## Command Reference

| Command | Description |
|---|---|
| `rootaccess login` | Log in via web browser OAuth flow |
| `rootaccess logout` | Clear local session credentials |
| `rootaccess whoami` | View current logged-in user and role |
| `rootaccess version` | Print CLI version and build metadata |
| `rootaccess contests` | List active and upcoming contests |
| `rootaccess contests join <ID>` | Register team for a contest |
| `rootaccess contests leave <ID>` | Unregister team from a contest |
| `rootaccess challenges [--contest <ID>]` | List challenges with solve counts and points |
| `rootaccess open <ID> [--contest <ID>]` | View full challenge description and files |
| `rootaccess submit <ID> <FLAG> [--contest <ID>]` | Submit a flag for validation |
| `rootaccess scoreboard` | Display the platform/contest scoreboard |
| `rootaccess collab challenge add <ID> [flags]` | Add a question with files and markdown descriptions |
| `rootaccess collab challenge upload <ID> <FILE>` | Upload file to contest storage (50 MB file / 500 MiB quota) |
| `rootaccess collab challenge list <ID>` | List all questions in a contest for collaborator/admin |
| `rootaccess collab request` | Submit contest hosting request |
| `rootaccess collab requests` | Check contest hosting request status |
| `rootaccess collab contests` | List contests you manage |
| `rootaccess collab invite accept <TOKEN>` | Accept contest collaborator invite |

---

## Configuration

Credentials and configuration are stored at:
- **Linux / macOS**: `~/.config/rootaccess/config.json`
- **Windows**: `%USERPROFILE%\.config\rootaccess\config.json`

The CLI connects to `https://ctf.rootaccess.live/api` by default.

---

## Documentation

Full documentation and guides are available at the **[RootAccess Docs](https://ctf.rootaccess.live/docs/cli-commands)**.

---

## License

This project is licensed under the [MIT License](LICENSE).
