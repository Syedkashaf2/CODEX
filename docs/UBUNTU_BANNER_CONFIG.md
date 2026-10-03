# 🎨 CODEX Banner Configuration Guide for Ubuntu

After installing CODEX on Ubuntu, you can customize your terminal banner in several ways. Here's a complete guide to modify and personalize your banner.

---

## 📍 Configuration Files Location

```bash
# Main configuration directory
~/.codex/

# Configuration files
~/.codex/config.conf           # Main settings
~/.codex/themes/               # Theme files
~/.codex/banner.conf           # Banner-specific config
~/.oh-my-zsh/themes/codex.zsh-theme  # ZSH theme file
~/.zshrc                       # Shell configuration
```

---

## 🔧 Method 1: Edit Banner Configuration File (Easiest)

### Step 1: Open the Banner Config
```bash
nano ~/.codex/banner.conf
```

### Step 2: Customize Your Banner Settings

Here's a sample banner.conf with all available options:

```bash
# CODEX Banner Configuration
# Last Updated: 2026-10-03

# ====== BANNER DISPLAY ======
BANNER_NAME="YOUR-NAME"           # Your custom banner name (max 8 chars)
BANNER_STYLE="box"                # box, flat, ascii, neon
BANNER_ENABLED="true"             # true/false to show/hide banner

# ====== COLOR SCHEME ======
COLOR_THEME="default"             # default, neon, hacker, matrix, ocean, sunset
PRIMARY_COLOR="cyan"              # cyan, green, yellow, magenta, blue, white
ACCENT_COLOR="green"              # Color for highlights
BACKGROUND="black"                # Terminal background color

# ====== ASCII ART ======
ASCII_MODE="enabled"              # enabled/disabled
ASCII_STYLE="kang"                # kang, simple, detailed, minimal
ANIMATION="none"                  # none, typing, fade, blink

# ====== SYSTEM INFO ======
SHOW_HOSTNAME="true"              # Display hostname
SHOW_KERNEL="true"                # Display kernel version
SHOW_UPTIME="true"                # Display system uptime
SHOW_PACKAGES="true"              # Display package count
SHOW_SHELL="true"                 # Display shell type
SHOW_CPU="true"                   # Display CPU info
SHOW_RAM="true"                   # Display RAM info

# ====== BANNER CONTENT ======
BANNER_MESSAGE="Hey Dear"         # Custom welcome message
SHOW_TELEGRAM="true"              # Show Telegram link
TELEGRAM_CHANNEL="t.me/KangCodex" # Your Telegram channel
SHOW_SOCIAL="true"                # Show social links

# ====== TIMING & ANIMATION ======
BANNER_DELAY="0"                  # Delay before showing banner (seconds)
TYPE_SPEED="0.02"                 # Typing animation speed
REFRESH_ON_LOGIN="true"           # Refresh banner on each login
```

### Step 3: Apply Changes
```bash
# Reload your shell configuration
source ~/.zshrc

# Open a new terminal tab to see changes
```

---

## 🎨 Method 2: Quick Banner Name Change

The fastest way to change just your banner name:

```bash
# Interactive mode (recommended)
codex-bname

# OR directly set the name
echo "YOUR-NAME" > ~/.codex/BANNER_NAME

# Apply changes
source ~/.zshrc
```

**Example:**
```bash
echo "NINJA" > ~/.codex/BANNER_NAME
source ~/.zshrc
```

---

## 🌈 Method 3: Change Theme/Color Scheme

### Option A: Using Theme Manager Command
```bash
# List all available themes
codex-theme list

# Apply a theme
codex-theme apply neon

# Create custom theme
codex-theme create "my-theme"
```

### Option B: Manually Edit Theme File

Create a new theme in `~/.codex/themes/`:

```bash
cat > ~/.codex/themes/my-custom-theme.conf <<'EOF'
# My Custom Theme
PRIMARY_COLOR="magenta"
ACCENT_COLOR="cyan"
BACKGROUND="black"
BANNER_STYLE="neon"
ASCII_STYLE="detailed"
COLOR_THEME="my-custom-theme"
EOF
```

Then activate it:
```bash
echo "COLOR_THEME=my-custom-theme" >> ~/.codex/banner.conf
source ~/.zshrc
```

---

## 🎯 Method 4: Edit ZSH Theme File Directly

For advanced customization, edit the theme file directly:

```bash
nano ~/.oh-my-zsh/themes/codex.zsh-theme
```

Key sections to modify:

```bash
# Color definitions
CODEX_CYAN='\033[1;96m'
CODEX_GREEN='\033[1;92m'
CODEX_YELLOW='\033[1;93m'
CODEX_RED='\033[1;91m'
CODEX_MAGENTA='\033[1;95m'
CODEX_BLUE='\033[1;94m'

# Modify the prompt
PROMPT='${CODEX_CYAN}[${CODEX_GREEN}DX${CODEX_CYAN}] %n@%m$ ${RESET}'

# Add custom banner function
show_banner() {
    echo -e "${CODEX_CYAN}Your Custom Banner Here${RESET}"
}
```

---

## 🛠️ Method 5: Edit Main Shell Configuration

Edit your `.zshrc` file for deeper customization:

```bash
nano ~/.zshrc
```

Look for the CODEX section and modify:

```bash
# ===== CODEX CUSTOMIZATION =====
export CODEX_HOME="$HOME/.codex"
export CODEX_BANNER_NAME="YOUR-NAME"
export CODEX_THEME="neon"

# Custom functions
show_codex_banner() {
    clear
    echo -e "\033[1;96m╔════════════════════════════════════╗\033[0m"
    echo -e "\033[1;96m║   \033[1;92m⚡ CODEX TERMINAL ⚡\033[1;96m   ║\033[0m"
    echo -e "\033[1;96m║   \033[1;93mWelcome: $CODEX_BANNER_NAME\033[1;96m   ║\033[0m"
    echo -e "\033[1;96m╚════════════════════════════════════╝\033[0m"
    echo
}

# Call it on shell start
show_codex_banner
```

---

## 🎨 Preset Color Schemes

### Default Theme
```bash
PRIMARY_COLOR="cyan"
ACCENT_COLOR="green"
```

### Neon Theme
```bash
PRIMARY_COLOR="magenta"
ACCENT_COLOR="cyan"
BANNER_STYLE="neon"
```

### Hacker Theme
```bash
PRIMARY_COLOR="green"
ACCENT_COLOR="black"
BACKGROUND="black"
BANNER_STYLE="ascii"
```

### Matrix Theme
```bash
PRIMARY_COLOR="green"
ACCENT_COLOR="cyan"
BANNER_STYLE="ascii"
ASCII_STYLE="detailed"
```

### Ocean Theme
```bash
PRIMARY_COLOR="blue"
ACCENT_COLOR="cyan"
BANNER_STYLE="box"
```

### Sunset Theme
```bash
PRIMARY_COLOR="yellow"
ACCENT_COLOR="magenta"
BANNER_STYLE="flat"
```

---

## 🎭 ASCII Art Styles

### Change ASCII Art Style

Edit `~/.codex/banner.conf`:

```bash
# Minimal ASCII
ASCII_STYLE="minimal"
BANNER_STYLE="flat"

# Detailed ASCII
ASCII_STYLE="detailed"
BANNER_STYLE="ascii"

# Box Drawing
ASCII_STYLE="box"
BANNER_STYLE="box"

# Simple
ASCII_STYLE="simple"
BANNER_STYLE="flat"
```

### Custom ASCII Art

Create custom ASCII and add to banner:

```bash
cat > ~/.codex/custom-banner.txt <<'EOF'
╔══════════════════════╗
║   ⚡ CODEX ULTRA ⚡  ║
║   Your Custom Name   ║
╚══════════════════════╝
EOF
```

Then reference in `~/.codex/banner.conf`:
```bash
CUSTOM_BANNER_FILE="$HOME/.codex/custom-banner.txt"
USE_CUSTOM_BANNER="true"
```

---

## 🔄 Method 6: Using Command Line Arguments

Quick one-time customization:

```bash
# Set banner name temporarily
CODEX_BANNER_NAME="ADMIN" zsh

# Set theme temporarily
CODEX_THEME="neon" zsh

# Set multiple options
CODEX_BANNER_NAME="NINJA" CODEX_THEME="hacker" zsh
```

---

## 🛡️ Method 7: System Info Display Customization

Control what information appears in your banner:

Edit `~/.codex/banner.conf`:

```bash
# Show/hide system information
SHOW_HOSTNAME="true"
SHOW_KERNEL="true"
SHOW_UPTIME="true"
SHOW_PACKAGES="true"
SHOW_SHELL="true"
SHOW_CPU="true"
SHOW_RAM="true"
SHOW_DISK="true"
SHOW_DATE="true"
SHOW_TIME="true"
```

---

## 🔐 Backup & Restore Configuration

### Backup Current Config
```bash
cp ~/.codex/banner.conf ~/.codex/banner.conf.backup
cp ~/.zshrc ~/.zshrc.backup
```

### Restore from Backup
```bash
cp ~/.codex/banner.conf.backup ~/.codex/banner.conf
source ~/.zshrc
```

### Create Named Config Snapshot
```bash
mkdir -p ~/.codex/configs
cp ~/.codex/banner.conf ~/.codex/configs/work-setup.conf
cp ~/.codex/banner.conf ~/.codex/configs/gaming-setup.conf
```

---

## 📋 Common Customization Examples

### Example 1: Minimal Developer Setup
```bash
cat > ~/.codex/banner.conf <<'EOF'
BANNER_NAME="DEV"
COLOR_THEME="hacker"
PRIMARY_COLOR="green"
BANNER_STYLE="flat"
SHOW_HOSTNAME="true"
SHOW_CPU="true"
SHOW_RAM="true"
SHOW_TIME="true"
SHOW_TELEGRAM="false"
EOF
source ~/.zshrc
```

### Example 2: Colorful Cyberpunk Setup
```bash
cat > ~/.codex/banner.conf <<'EOF'
BANNER_NAME="CYBER"
COLOR_THEME="neon"
PRIMARY_COLOR="magenta"
ACCENT_COLOR="cyan"
BANNER_STYLE="neon"
ASCII_STYLE="detailed"
ANIMATION="typing"
SHOW_SOCIAL="true"
EOF
source ~/.zshrc
```

### Example 3: Corporate Professional Setup
```bash
cat > ~/.codex/banner.conf <<'EOF'
BANNER_NAME="WORK"
COLOR_THEME="ocean"
PRIMARY_COLOR="blue"
BANNER_STYLE="box"
ASCII_STYLE="minimal"
SHOW_HOSTNAME="true"
SHOW_TELEGRAM="false"
SHOW_SOCIAL="false"
BANNER_MESSAGE="Welcome to Work Terminal"
EOF
source ~/.zshrc
```

### Example 4: Gaming/Fun Setup
```bash
cat > ~/.codex/banner.conf <<'EOF'
BANNER_NAME="GAMER"
COLOR_THEME="matrix"
PRIMARY_COLOR="green"
ACCENT_COLOR="black"
BANNER_STYLE="ascii"
ASCII_STYLE="detailed"
ANIMATION="fade"
BANNER_MESSAGE="Let's Game!"
SHOW_CPU="true"
EOF
source ~/.zshrc
```

---

## 🔧 Troubleshooting Configuration Issues

### Colors Not Showing
```bash
# Check if terminal supports 256 colors
echo $TERM

# Force colors
export TERM=xterm-256color
source ~/.zshrc
```

### Banner Not Appearing
```bash
# Check if configuration is loaded
cat ~/.codex/banner.conf

# Manually trigger banner
source ~/.oh-my-zsh/themes/codex.zsh-theme

# Reset to defaults
codex-reset
```

### Changes Not Applied
```bash
# Clear any shell caches
hash -r

# Reload shell completely
exec zsh
```

---

## 🚀 Advanced Tips

### Tip 1: Create Dynamic Banner
```bash
# Edit ~/.zshrc to add dynamic content
precmd() {
    CURRENT_TIME=$(date "+%H:%M")
    export CODEX_BANNER_NAME="DEV-$CURRENT_TIME"
}
```

### Tip 2: Multiple Profiles
```bash
# Create different config files
~/.codex/banner-work.conf
~/.codex/banner-home.conf
~/.codex/banner-gaming.conf

# Switch between them
codex-profile switch work
codex-profile switch home
```

### Tip 3: Conditional Banner Display
```bash
# Show different banner based on SSH
if [ -n "$SSH_CLIENT" ]; then
    export CODEX_BANNER_NAME="REMOTE"
else
    export CODEX_BANNER_NAME="LOCAL"
fi
```

---

## 📞 Getting Help

```bash
# View all banner options
codex-help banner

# Check configuration status
codex-config check

# Validate configuration
codex-config validate

# Show current theme
codex-theme current

# List available themes
codex-theme list
```

---

## ✅ Quick Checklist for First-Time Setup

- [ ] Opened `~/.codex/banner.conf`
- [ ] Changed `BANNER_NAME` to your preferred name
- [ ] Selected a `COLOR_THEME` you like
- [ ] Set `PRIMARY_COLOR` and `ACCENT_COLOR`
- [ ] Saved the file (Ctrl+O, Enter, Ctrl+X in nano)
- [ ] Ran `source ~/.zshrc`
- [ ] Opened a new terminal tab to see changes
- [ ] Created a backup with `cp ~/.codex/banner.conf ~/.codex/banner.conf.backup`

---

## 🎯 Next Steps

After configuring your banner:
1. Learn about **[Theme Management](./UBUNTU_THEME_GUIDE.md)**
2. Explore **[Advanced Customization](./UBUNTU_ADVANCED.md)**
3. Check **[Troubleshooting](./TROUBLESHOOTING.md)**
4. View **[All Available Commands](./UBUNTU_COMMANDS.md)**

---

**Happy Customizing! 🚀**
