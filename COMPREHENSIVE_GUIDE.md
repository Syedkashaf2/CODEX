# 🚀 CODEX - Complete Configuration & Installation Guide

**Version**: 2.0.0  
**Last Updated**: 2026-10-03  
**Status**: Advanced Documentation

---

## 📋 Table of Contents

1. [Quick Start](#quick-start)
2. [System Requirements](#system-requirements)
3. [Installation Guide](#installation-guide)
4. [Configuration Guide](#configuration-guide)
5. [AutoComplete & Shell Enhancement](#autocomplete--shell-enhancement)
6. [Advanced Features](#advanced-features)
7. [Command Reference](#command-reference)
8. [Troubleshooting](#troubleshooting)
9. [Removal & Restoration](#removal--restoration)
10. [FAQ](#faq)

---

## 🎯 Quick Start

### For Impatient Users (30 seconds)

#### **Termux (Android)**
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/Syedkashaf2/CODEX/main/install.sh)
```

#### **Linux**
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/Syedkashaf2/CODEX/main/install.sh)
```

**That's it!** Your terminal will be transformed. Follow the on-screen prompts to set your banner name.

---

## 📱 System Requirements

### Minimum Requirements
| Requirement | Version | Purpose |
|-------------|---------|---------|
| **OS** | Termux or Linux | Main environment |
| **Bash** | 4.0+ | Script execution |
| **curl** | Any recent | Downloads |
| **git** | 2.0+ | Version control |
| **ncurses-utils** | Any | Terminal utilities |

### Optional (Recommended for Full Features)
| Package | Purpose |
|---------|---------|
| **Python 3.6+** | AI Chat, advanced features |
| **Ruby** | Enhanced text formatting |
| **jq** | JSON parsing |
| **lsd** | Advanced file listing |
| **figlet** | ASCII art generation |
| **zsh** | Advanced shell features |

### Disk Space
- **Minimum**: ~50MB for installation
- **Recommended**: 100MB+ for optimal performance with all features

---

## 📥 Installation Guide

### 🔷 Method 1: Automatic Installation (Recommended)

#### Step 1: Clone Repository
```bash
git clone https://github.com/Syedkashaf2/CODEX.git
cd CODEX
```

#### Step 2: Run Installer
```bash
bash install.sh
```

#### Step 3: Follow On-Screen Setup
- The installer will auto-detect your system (Termux or Linux)
- It will install all required dependencies
- You'll be prompted to enter your **Banner Name** (1-8 characters, alphanumeric only)

#### Step 4: Verify Installation
```bash
help
```

---

### 🔷 Method 2: Direct Installation via curl
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/Syedkashaf2/CODEX/main/install.sh)
```

---

### 🔷 Method 3: Manual Installation

#### For Termux:
```bash
# Update packages
pkg update -y && pkg upgrade -y

# Install dependencies
pkg install -y git curl ncurses-utils jq python zsh ruby

# Clone repository
git clone https://github.com/Syedkashaf2/CODEX.git
cd CODEX

# Run installer
bash install.sh
```

#### For Linux (Ubuntu/Debian):
```bash
# Update packages
sudo apt update -y && sudo apt upgrade -y

# Install dependencies
sudo apt install -y git curl ncurses-bin jq python3 python3-pip zsh ruby

# Clone repository
git clone https://github.com/Syedkashaf2/CODEX.git
cd CODEX

# Run installer (will ask for sudo when needed)
bash install.sh
```

---

## ⚙️ Configuration Guide

### 🎨 Banner Configuration

#### Change Banner Name
```bash
bname
```

**Interactive Prompt:**
```
Enter Your Banner Name: YOUR_NAME
(Must be 1-8 alphanumeric characters)
```

**What It Does:**
- Updates your terminal prompt/banner with your custom name
- Personalizes your shell greeting
- Maximum 8 characters for optimal display

#### Example:
```bash
$ bname
> Enter Your Name: HACKER
# Your banner now displays "HACKER" instead of "DX-SIMU"
```

---

### 🎭 Theme Configuration

#### View Available Themes
```bash
themes -l
```

#### Apply a Theme
```bash
themes apply dark-matrix
themes apply cyberpunk
themes apply hacker-green
```

#### Create Custom Theme
```bash
themes create "my-custom-theme"
```

**What Gets Customized:**
- Color scheme (30+ pre-configured)
- Prompt appearance
- Banner styling
- Syntax highlighting colors

---

### 🔧 Configuration Files

#### Main Configuration
- **Path**: `$HOME/.zshrc`
- **Contains**: Shell settings, aliases, plugins
- **Edit**: `config edit` or manually edit with `nano ~/.zshrc`

#### Theme Configuration
- **Path**: `$HOME/.oh-my-zsh/themes/codex.zsh-theme`
- **Contains**: Theme variables and styling
- **Edit**: `nano ~/.oh-my-zsh/themes/codex.zsh-theme`

#### Custom Configuration Directories
- **Termux**: `$HOME/.termux/`
- **Linux**: `$HOME/.CODEX/`
- **Tools**: `$HOME/.toolx/`

#### Configuration Commands
```bash
# Edit configuration
config edit

# Reset to defaults
config reset

# Validate configuration
config validate

# Sync across devices
config sync
```

---

## 🤖 AutoComplete & Shell Enhancement

### 🔹 Built-in AutoComplete Features

#### 1. **ZSH AutoSuggestions** (Installed by Default)
- Provides command suggestions as you type
- Based on your command history
- Press `Tab` or right arrow to accept suggestions

```bash
$ gi  # Start typing
# Suggestion appears: "git commit -m"
# Press Tab or → to accept
```

**Configuration:**
```bash
# In ~/.zshrc
# Enable/Disable by modifying:
source $HOME/.oh-my-zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
```

---

#### 2. **ZSH Syntax Highlighting** (Installed by Default)
- Real-time syntax validation as you type
- Color-codes valid/invalid commands
- Highlights errors before execution

**Visual Feedback:**
```bash
$ echo "valid"      # Green text = valid command
$ echoo "invalid"   # Red text = invalid command
```

**Configuration:**
```bash
# In ~/.zshrc
source $HOME/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# Customize colors:
ZSH_HIGHLIGHT_STYLES[comment]='fg=blue'
ZSH_HIGHLIGHT_STYLES[alias]='fg=green,bold'
ZSH_HIGHLIGHT_STYLES[builtin]='fg=cyan'
```

---

#### 3. **Git Plugin AutoComplete**
- Auto-complete git commands and branches
- Supports: `git add`, `git commit`, `git push`, `git branch`, etc.

```bash
$ git ch<Tab>        # Auto-completes to 'git checkout'
$ git checkout br<Tab>  # Shows available branches
```

---

#### 4. **Oh My Zsh Framework Integration**
Provides advanced autocompletion for:
- Command options
- File paths
- Environment variables
- Directory navigation

```bash
# Example: cd with autocompletion
$ cd /home/us<Tab>   # Auto-completes to /home/username/

# Example: ls options
$ ls -<Tab>          # Shows all available ls options
```

---

### 🔹 Custom Alias Management

#### Add Custom Aliases
```bash
alias add myalias="command here"
```

**Example:**
```bash
alias add ll="ls -lah"
alias add gs="git status"
alias add gc="git commit -m"
alias add gp="git push"
```

#### List All Aliases
```bash
alias list
```

#### Remove Alias
```bash
alias remove ll
```

#### Export Aliases
```bash
alias export > my-aliases.conf
```

#### Restore Aliases
```bash
alias import < my-aliases.conf
```

---

### 🔹 Command Completion Customization

#### Add Custom Completion Functions

**Create completion script** at `$HOME/.oh-my-zsh/completions/my-completion.zsh`:

```bash
# Example completion for custom command
_my_command() {
    local commands=(
        'start:Start service'
        'stop:Stop service'
        'restart:Restart service'
        'status:Check status'
    )
    
    _describe 'command' commands
}

compdef _my_command my_command
```

#### Enable Completion
```bash
# Add to ~/.zshrc
fpath=($fpath $HOME/.oh-my-zsh/completions)
autoload -Uz compinit && compinit
```

---

## 🎯 Advanced Features

### 📊 System Monitoring

#### Real-Time Dashboard
```bash
monitor
```

#### CPU Statistics
```bash
monitor cpu
```

#### Memory Usage
```bash
monitor memory
```

#### Network Statistics
```bash
monitor network
```

**Output Includes:**
- CPU utilization percentage
- RAM usage and available memory
- Disk I/O statistics
- Network bandwidth
- Process information

---

### 💬 AI Chat Integration

#### Launch Chat
```bash
chat
```

**Features:**
- AI-powered terminal chat
- Real-time responses
- Command suggestions
- System information queries

**Example Usage:**
```bash
$ chat
[Chatbot]: Hello! How can I help?
[You]: How do I compress files in Linux?
[Chatbot]: Use tar command: tar -czf archive.tar.gz folder/
```

---

### 🔧 Git Assistant

#### Quick Git Operations
```bash
gitx commit "Your message"
gitx clone-setup <repo-url>
gitx status-full
```

#### Git Workflow Commands
```bash
# Initialize and setup
gitx init

# Quick commit
gitx commit "message"

# Push changes
gitx push

# View status with dashboard
gitx status-full
```

---

### 💾 Session Management

#### Backup Current Session
```bash
backup create session-name
```

#### Restore Session
```bash
backup restore session-name
```

#### List All Backups
```bash
backup list
```

#### Delete Backup
```bash
backup delete session-name
```

---

### 🎯 Hotkey Management

#### Configure Custom Hotkeys
```bash
hotkeys
```

**Common Hotkey Setups:**
```bash
# Open web browser
Ctrl+Alt+B : xdg-open https://github.com

# Clear screen with banner
Ctrl+L : clear

# Quick git status
Ctrl+G : git status
```

---

### 👤 Multi-Profile Support

#### Create Profile
```bash
profile create "work"
profile create "development"
```

#### Switch Profile
```bash
profile switch work
profile switch development
```

#### List Profiles
```bash
profile list
```

#### Delete Profile
```bash
profile delete work
```

---

## 📚 Command Reference

### 🔹 Core Commands

| Command | Syntax | Description |
|---------|--------|-------------|
| **help** | `help` | Display all available commands |
| **bname** | `bname` | Change terminal banner name |
| **update** | `update` | Update CODEX to latest version |
| **unstall** | `unstall` | Restore terminal to default state |
| **chat** | `chat` | Launch AI-powered chat |
| **dev** | `dev` or `report` | Developer info & bug reports |

### 🔹 Advanced Commands

| Command | Syntax | Description |
|---------|--------|-------------|
| **stats** | `stats` | Display system statistics |
| **monitor** | `monitor [cpu\|memory\|network]` | Real-time system monitoring |
| **themes** | `themes [list\|apply\|create]` | Theme management |
| **alias** | `alias [add\|remove\|list]` | Alias management |
| **hotkeys** | `hotkeys` | Configure keyboard shortcuts |
| **gitx** | `gitx [commit\|push\|status-full]` | Git assistant |
| **backup** | `backup [create\|restore\|list]` | Session management |
| **config** | `config [edit\|reset\|validate]` | Configuration management |
| **profile** | `profile [create\|switch\|list]` | Multi-profile support |

### 🔹 Mini Commands

| Command | Description |
|---------|-------------|
| `ls` | Enhanced file listing (lsd) |
| `lt` | Tree view of directory |
| `la` | List all files with details |
| `clear` | Clear screen with banner |
| `clear n` | Clear without banner |
| `exit` | Exit with animation |
| `exit x` | Advanced exit options |

---

## 🔧 Troubleshooting

### ❌ Issue: Installation Fails

**Error**: `curl: command not found`

**Solution**:
```bash
# Termux
pkg install curl -y

# Linux
sudo apt install curl -y
```

---

### ❌ Issue: Banner Not Displaying

**Error**: Characters or symbols not showing correctly

**Solution**:
1. **Termux**: Font automatically installed. Try `termux-reload-settings`
2. **Linux**: Install fonts:
```bash
# Check font installation
fc-list | grep -i nerd

# Reinstall fonts
~/.local/share/fonts/
# Place .ttf files here and run:
fc-cache -fv
```

---

### ❌ Issue: AutoComplete Not Working

**Error**: Tab key not suggesting commands

**Solution**:
```bash
# Reload zsh configuration
exec zsh

# Or manually source
source ~/.zshrc

# Verify plugins loaded
echo $PLUGINS
```

---

### ❌ Issue: Performance Slow

**Error**: Terminal responds slowly to commands

**Solution**:
1. **Reduce loaded plugins** in `~/.zshrc`:
```bash
# Comment out unnecessary plugins
plugins=(git)  # Keep essential only
```

2. **Disable auto-update checks**:
```bash
# In ~/.zshrc, add:
DISABLE_AUTO_UPDATE="true"
```

3. **Reduce theme complexity**:
```bash
themes apply simple
```

---

### ❌ Issue: SSH Issues in Git

**Error**: `Permission denied (publickey)`

**Solution**:
```bash
# Generate SSH key (if not exists)
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa

# Add to git hosting (GitHub, GitLab, etc.)
cat ~/.ssh/id_rsa.pub

# Test connection
ssh -T git@github.com
```

---

### ❌ Issue: Theme Not Applying

**Error**: `Theme not found` or wrong colors

**Solution**:
```bash
# Check theme location
ls ~/.oh-my-zsh/themes/

# Manually set theme in ~/.zshrc
ZSH_THEME="codex"

# Reload
exec zsh
```

---

## 🗑️ Removal & Restoration

### ⚠️ Complete Removal

#### Method 1: Using Built-in Uninstall
```bash
unstall
```

**Interactive Confirmation**:
```
Do you want to restore the default terminal?
Type 'y' or 'yes' to continue: y
```

**What Gets Removed**:
- ✅ Oh My Zsh framework
- ✅ ZSH configuration files
- ✅ All CODEX tools and scripts
- ✅ Custom themes and colors
- ✅ Alias configurations
- ✅ Custom fonts

#### Method 2: Manual Removal

**For Termux**:
```bash
# Remove shell config
rm -rf ~/.oh-my-zsh ~/.zshrc ~/.zsh_history

# Remove CODEX directories
rm -rf ~/.toolx ~/.Codex-simu ~/.CODEX

# Remove custom styles
rm -f ~/.termux/font.ttf ~/.termux/colors.properties

# Reset to bash
chsh -s bash

# Reload settings
termux-reload-settings
```

**For Linux**:
```bash
# Remove shell config
rm -rf ~/.oh-my-zsh ~/.zshrc ~/.zsh_history

# Remove CODEX directories
rm -rf ~/.toolx ~/.Codex-simu ~/.CODEX

# Remove system fonts
sudo rm -f /usr/share/figlet/ASCII-Shadow.flf

# Reset to bash
sudo chsh -s /bin/bash $USER

# Refresh fonts
fc-cache -fv
```

---

### 🔄 Restore Only Configuration (Keep Shell)

**Keep enhanced shell, restore default theme**:
```bash
# Reset theme to default
ZSH_THEME="robbyrussell"  # In ~/.zshrc

# Remove CODEX theme
rm ~/.oh-my-zsh/themes/codex.zsh-theme

# Reload
exec zsh
```

---

## ❓ FAQ

### Q1: Can I use CODEX with Fish or Bash?
**A**: Currently optimized for ZSH. Bash support is in the roadmap. You can still use basic features without ZSH, but many advanced features require ZSH.

```bash
# Check current shell
echo $SHELL

# Switch to ZSH
chsh -s zsh
```

---

### Q2: How do I backup my configuration?
**A**: Use the built-in backup system:
```bash
# Create backup
backup create my-config

# Restore from backup
backup restore my-config

# List all backups
backup list
```

**Manual backup**:
```bash
cp -r ~/.zshrc ~/.oh-my-zsh ~/codex-backup/
```

---

### Q3: Does CODEX work on other Linux distros?
**A**: Yes! Tested on:
- ✅ Ubuntu/Debian
- ✅ Arch Linux
- ✅ CentOS/RHEL
- ✅ Fedora
- ✅ Termux (Android)

Minor adjustments may be needed for package managers other than `apt`.

---

### Q4: Can I customize the colors?
**A**: Yes! Edit theme file:
```bash
nano ~/.oh-my-zsh/themes/codex.zsh-theme
```

**Or create custom theme**:
```bash
themes create my-theme
```

---

### Q5: How often should I update CODEX?
**A**: 
- **Auto-update**: Enabled by default (checks on shell start)
- **Manual update**: `update` command
- **Check version**: `codex --version`

**Disable auto-update**:
```bash
# In ~/.zshrc, add:
CODEX_AUTO_UPDATE="false"
```

---

### Q6: Is CODEX safe? Does it track data?
**A**: 
- ✅ **Open-source**: Full code available
- ✅ **No telemetry**: Zero tracking
- ✅ **Local storage only**: Everything stays on your device
- ✅ **MIT Licensed**: Free for personal and commercial use

---

### Q7: How do I report bugs?
**A**: Use the `dev` command:
```bash
dev
```

**Or manually**:
- Visit: https://github.com/Syedkashaf2/CODEX/issues
- Telegram: https://t.me/KangCodex

---

### Q8: Can I modify the source code?
**A**: Yes! It's MIT licensed:
```bash
# Fork the repository
git clone https://github.com/YOUR_USERNAME/CODEX.git

# Make changes
# Submit pull request
```

---

## 📞 Support & Community

### 🔗 Links
- **GitHub**: https://github.com/Syedkashaf2/CODEX
- **Telegram Channel**: https://t.me/KangCodex
- **Issues Tracker**: https://github.com/Syedkashaf2/CODEX/issues
- **Original Source**: https://github.com/Alpha-Codex369/CODEX

### 📝 Report Bugs
```bash
dev
# or
report
```

---

## 📈 Roadmap

- [ ] Cloud sync feature for multi-device setup
- [ ] Mobile app companion
- [ ] Web-based dashboard
- [ ] Plugin marketplace
- [ ] Team collaboration features
- [ ] Multi-shell support (bash, zsh, fish)
- [ ] Advanced debugging tools
- [ ] Machine learning-powered command suggestions

---

## 📄 License

CODEX is licensed under the **MIT License** - see LICENSE file for details.

---

## 🙏 Credits

- **Creator**: KANG
- **Original Project**: Alpha-Codex369
- **Community Contributors**: Open Source Community
- **Inspired by**: iTerm2, Powerlevel10k, Oh My Zsh

---

**Last Updated**: 2026-10-03  
**Version**: 2.0.0  
**Status**: Actively Maintained ✅

---

**Happy Coding! 🚀**
