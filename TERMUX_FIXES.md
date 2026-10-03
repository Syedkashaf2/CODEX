# 🔧 CODEX Termux Setup Fixes & AutoComplete Guide

## 🔴 Fix 1: Corrupt `.termux` Directory Issue

The `.termux` should be a **directory**, not a file. If it was showing as a file, here's how to properly fix it:

### Permanent Fix

```bash
# 1. Backup current config
cp ~/.termux/colors.properties ~/colors_backup.properties 2>/dev/null || true

# 2. Remove the corrupted file
rm -f ~/.termux

# 3. Create proper directory
mkdir -p ~/.termux

# 4. Restore or recreate color scheme
cat > ~/.termux/colors.properties << 'EOF'
background=#000000
foreground=#ffffff
cursor=#ffffff
color0=#000000
color1=#ff0000
color2=#00ff00
color3=#ffff00
color4=#0000ff
color5=#ff00ff
color6=#00ffff
color7=#ffffff
color8=#808080
color9=#ff0000
color10=#00ff00
color11=#ffff00
color12=#0000ff
color13=#ff00ff
color14=#00ffff
color15=#ffffff
EOF

# 5. Copy font file (if it exists in CODEX)
cp ~/CODEX/files/font.ttf ~/.termux/ 2>/dev/null || true

# 6. Reload settings
termux-reload-settings

# 7. Test
echo "✓ .termux directory fixed"
```

### Verify It's Fixed

```bash
ls -la ~/.termux/
# Should show a directory (drwx------) with files inside:
# - colors.properties
# - font.ttf
# - usernames.txt (created during setup)
```

---

## 🔴 Fix 2: AutoComplete Not Working

ZSH autosuggestions require proper plugin installation. Here's the complete fix:

### Step 1: Verify Plugins Are Installed

```bash
# Check if plugins directory exists
ls -la ~/.oh-my-zsh/plugins/ | grep -E "zsh-autosuggestions|zsh-syntax-highlighting"
```

**Expected output:**
```
drwxr-xr-x zsh-autosuggestions
drwxr-xr-x zsh-syntax-highlighting
```

### Step 2: If Plugins Are Missing, Install Them

```bash
# Install zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ~/.oh-my-zsh/plugins/zsh-autosuggestions

# Install zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
  ~/.oh-my-zsh/plugins/zsh-syntax-highlighting

# Verify installation
ls ~/.oh-my-zsh/plugins/zsh-autosuggestions/
ls ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/
```

### Step 3: Update ~/.zshrc to Enable Plugins

```bash
# Open the file
nano ~/.zshrc
```

**Find this section** (around line 17):
```bash
plugins=(git)
```

**Replace it with:**
```bash
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

**Also ADD these lines at the END of ~/.zshrc** (before any source commands):

```bash
# ============= AutoComplete Configuration =============
# Source autosuggestions plugin
if [ -f ~/.oh-my-zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh ]; then
    source ~/.oh-my-zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
fi

# Source syntax highlighting plugin
if [ -f ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ]; then
    source ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
fi

# AutoSuggest Configuration
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=8"  # Gray suggestions
ZSH_AUTOSUGGEST_STRATEGY=(history completion)
ZSH_AUTOSUGGEST_BUFFER_MAX_SIZE=20

# Syntax Highlighting Configuration
ZSH_HIGHLIGHT_STYLES[comment]='fg=blue'
ZSH_HIGHLIGHT_STYLES[alias]='fg=green,bold'
ZSH_HIGHLIGHT_STYLES[builtin]='fg=cyan'
ZSH_HIGHLIGHT_STYLES[command]='fg=green'
```

**Save and exit** (Ctrl+X, then Y, then Enter)

### Step 4: Reload Shell

```bash
exec zsh
```

### Step 5: Test AutoComplete

```bash
# Type this and press Tab to see suggestions:
git 
# Should show suggestions like: git add, git commit, git push, etc.

# Type partial command and press Tab:
echo "
# Should auto-complete if history contains it

# Type a directory and press Tab:
cd /data
# Should show suggestions for /data/data, etc.
```

---

## 🟢 AutoComplete Features Explained

### 1. **ZSH AutoSuggestions** (Grayed out text)

As you type, zsh shows suggestions based on your command history.

**Usage:**
```bash
$ git c
           # (gray suggestion appears: git commit)
# Press Tab or Right Arrow → to accept
$ git commit
```

**Customize Suggestion Color:**

Edit `~/.zshrc` and change:
```bash
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=8"  # Gray (default)
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=7"  # White
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=6"  # Cyan
```

### 2. **ZSH Syntax Highlighting** (Colored text)

Commands are highlighted in real-time:
- **Green** = valid command
- **Red** = invalid command
- **Cyan** = builtin command
- **Blue** = comment

```bash
$ echo "hello"    # Green (valid)
$ echoo "hello"   # Red (invalid - typo)
$ cd /home        # Cyan (valid builtin)
```

### 3. **Git AutoComplete**

Complete git commands and branches:

```bash
$ git ch<Tab>           # → git checkout
$ git checkout br<Tab>  # → git checkout branch-name
$ git co<Tab>           # → git commit or git config
```

### 4. **Command Option AutoComplete**

Complete command options:

```bash
$ ls -<Tab>
# Shows all ls options:
# --all  --author  --block-size  --color ...

$ grep -<Tab>
# Shows all grep options:
# -c  -E  -F  -G  -H ...
```

---

## 🟡 Advanced AutoComplete Customization

### Add Custom Completions

Create a file `~/.oh-my-zsh/completions/my-custom.zsh`:

```bash
# Example: Custom completion for 'docker' commands
_docker_commands() {
    local commands=(
        'build:Build an image from a Dockerfile'
        'run:Run a command in a new container'
        'ps:List containers'
        'images:List images'
        'logs:Fetch logs of a container'
        'exec:Execute a command in a running container'
    )
    _describe 'docker command' commands
}

compdef _docker_commands docker
```

Then add to `~/.zshrc`:
```bash
fpath=(~/.oh-my-zsh/completions $fpath)
autoload -Uz compinit && compinit
```

### Disable AutoComplete for Specific Commands

Add to `~/.zshrc`:
```bash
# Disable autocomplete for certain commands
compdef -d mycommand
```

### Speed Up AutoComplete

```bash
# In ~/.zshrc, add:
# Lazy-load completions
autoload -Uz compinit
if [[ -n ${ZDOTDIR}/.zcompdump(Nmh+24) ]]; then
    compinit
else
    compinit -C
fi
```

---

## 🔧 Troubleshooting AutoComplete

### ❌ AutoComplete Still Not Working After Changes

```bash
# 1. Clear ZSH completion cache
rm -f ~/.zcompdump*

# 2. Force recompile
compinit -u

# 3. Reload shell
exec zsh
```

### ❌ AutoComplete Suggestions Are Slow

```bash
# Reduce history size in ~/.zshrc
HISTSIZE=5000
SAVEHIST=5000

# Disable expensive completion strategies
ZSH_AUTOSUGGEST_STRATEGY=()  # Disables all strategies (empty)
# Or use only history:
ZSH_AUTOSUGGEST_STRATEGY=(history)
```

### ❌ Suggestion Color Not Visible

```bash
# Try different colors in ~/.zshrc
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=white,underline"
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=yellow"
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=magenta"

# Then reload
exec zsh
```

### ❌ Syntax Highlighting Not Showing Colors

```bash
# Make sure plugin is sourced at END of ~/.zshrc
source ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# Must be last line or near the end!
# Reload
exec zsh
```

---

## ✅ Complete AutoComplete Setup (Copy-Paste)

If you want to do everything at once:

```bash
# 1. Install plugins
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ~/.oh-my-zsh/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
  ~/.oh-my-zsh/plugins/zsh-syntax-highlighting

# 2. Update .zshrc
cat >> ~/.zshrc << 'EOF'

# ============= AutoComplete Config =============
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)

# AutoSuggest
if [ -f ~/.oh-my-zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh ]; then
    source ~/.oh-my-zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
fi

# Syntax Highlighting  
if [ -f ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ]; then
    source ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
fi

ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=8"
ZSH_AUTOSUGGEST_STRATEGY=(history completion)
EOF

# 3. Reload
exec zsh

# 4. Test
git <Tab>
```

---

## 📋 Quick Checklist

- [ ] Shell is set to zsh: `echo $SHELL` → should show `/data/data/com.termux/files/usr/bin/zsh`
- [ ] `.termux` is a directory: `ls -la ~/.termux/` → should show `drwx------`
- [ ] Plugins installed: `ls ~/.oh-my-zsh/plugins/` → should show both plugins
- [ ] Plugins sourced in `~/.zshrc` → manually added to end of file
- [ ] Shell reloaded: `exec zsh`
- [ ] AutoComplete works: `git <Tab>` → shows suggestions

---

**Last Updated**: 2026-10-03  
**Status**: Fully Fixed ✅
