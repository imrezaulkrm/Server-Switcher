# Server Switcher 🚀

**Interactive SSH Server Switcher** – Automatically detects servers from your `~/.ssh/config`, displays an **interactive fuzzy-search menu** (powered by [fzf](https://github.com/junegunn/fzf)), and connects via SSH with a **single selection**. 

Perfect for Linux power users managing multiple servers. **Zero typing, instant access!** ✨  

## ✨ Features

- 🔍 **Auto-detects** all servers from `~/.ssh/config` (ignores wildcards like `Host *`).
- 📊 **Shows total server count** for quick overview.
- 🎯 **Interactive fzf menu**: Arrow keys + type-to-search filtering.
- ⚡ **One-key SSH**: Runs `ssh <Host>` – auto-loads username, port, etc., from config.
- 🌐 **System-wide install** (`/usr/local/bin/server`) for global access.
- 🪶 **Lightweight & reliable**: Pure Bash, no dependencies beyond fzf.

## 📋 Requirements
- **fzf** for fuzzy selection.

### Install fzf

```bash
# Ubuntu/Debian
sudo apt update && sudo apt install fzf -y

# Fedora/RHEL
sudo dnf install fzf -y

# macOS (Homebrew)
brew install fzf

# Arch Linux
sudo pacman -S fzf
```

> **Pro Tip**: A valid `~/.ssh/config` with `Host` entries (example below).

## 🚀 Quick Install (GitHub Clone & Setup)

1. **Clone the repo**:
   ```bash
   git clone https://github.com/YOUR-USERNAME/server-switcher.git
   cd server-switcher
   ```

2. **Install system-wide**:
   ```bash
   sudo mv server /usr/local/bin/server
   sudo chmod +x /usr/local/bin/server
   ```

3. **Verify PATH** (usually auto-included):
   ```bash
   echo $PATH | grep /usr/local/bin
   ```
   *If missing*:
   ```bash
   echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bashrc  # or ~/.zshrc
   source ~/.bashrc
   ```

> 🎉 **Done!** Type `server` to launch.

## 🔧 SSH Config Setup

Edit `~/.ssh/config` (create if missing):

```bash
HOST "NAME"
    HOSTNAME "HOST IP OR DOMAIN"
    USER "USERNAME"
    Port "SERVER SSH PORT"
```

**Key Notes**:
- Script parses **only `Host` lines** for selection.
- All other directives (User, Port, etc.) are auto-applied by SSH.
- Supports **keys, proxies, etc.** – full SSH config power!

## 🎮 Usage

1. Run:
   ```bash
   server
   ```

2. **Interactive Menu** appears:
   ```
   > monitoring    (2 servers found)
     netbox
     production-db
   ```

   - **↑↓ arrows** or **type to filter** (fzf magic!).
   - **Enter** to connect.

3. **Auto-runs**:
   ```bash
   ssh monitoring  # Uses your config seamlessly
   ```

## ⚡ Optional: Short Alias

```bash
echo "alias ss='server'" >> ~/.bashrc  # or ~/.zshrc
source ~/.bashrc
```

Now: `ss` → instant menu! 🪄

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| `fzf: command not found` | Install fzf (see Requirements). |
| `No hosts found!` | Add `HOST` entries to `~/.ssh/config`. |
| `Permission denied` | `chmod +x /usr/local/bin/server`. |
| `Command not found` | Add `/usr/local/bin` to `$PATH`. |
| Slow menu? | Update fzf: `fzf --version`. |

**Debug**: Run `server --debug` (if script supports; else `cat ~/.ssh/config`).

## 🔍 How It Works (Under the Hood)

1. **Parse** `~/.ssh/config` → Extract `Host` names.
2. **Pipe to fzf** → Interactive preview/multi-select ready.
3. **Select → Exec** `ssh $selected_host`.

**Pure Bash magic** – ~50 lines, blazing fast. 📈

**Star the repo, fork it, contribute!** Questions? Open an issue.

---

## Folder Structure (GitHub)

server-switcher/
├── server           # Main bash script
├── README.md        # This guide
└── .gitignore       # Optional

## Quick Summary

1.  Clone repo
    
2.  Move `server` script to `/usr/local/bin`
    
3.  Add hosts to `~/.ssh/config`
    
4.  Run `server` (or alias `ss`)

Enjoy interactive SSH access!


# **Conclusion**

Server Switcher is a lightweight and interactive tool that makes SSH connections fast and effortless. By reading your `~/.ssh/config`, it automatically lists all servers, shows the total count, and allows you to connect with a single selection. With minimal setup, system-wide installation, and optional alias support, it simplifies server management for any user.
