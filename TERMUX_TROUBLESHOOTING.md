# 🔧 CODEX Termux Troubleshooting Guide

**Note**: CODEX is primarily designed for Termux. This guide covers 95% of Termux-specific issues.

---

## 🚨 Installation Issues

### ❌ Issue: "curl: command not found"

**Cause**: curl is not installed

**Solution**:
```bash
pkg install curl -y
```

Then retry installation:
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/Syedkashaf2/CODEX/main/install.sh)
```

---

### ❌ Issue: "git: command not found"

**Cause**: git is not installed

**Solution**:
```bash
pkg install git -y
```

---

### ❌ Issue: Permission Denied During Installation

**Cause**: Incorrect file permissions

**Solution**:
```bash
# Grant execute permissions
chmod +x install.sh

# Then run
bash install.sh
```

---

### ❌ Issue: "No space left on device"

**Cause**: Storage is full (common in Termux)

**Solution**:
```bash
# Check disk usage
df -h $HOME

# Clear cache
rm -rf ~/.cache ~/.local/share/cache

# Remove unnecessary files
rm -rf ~/Downloads/* ~/Documents/*

# Try installation again
```

---

### ❌ Issue: Network timeout during installation

**Cause**: Internet connection issue or slow connection

**Solution**:
```bash
# Check internet
ping github.com

# If no response, fix WiFi connection

# Retry with verbose output
bash install.sh -v

# If keeps timing out, try manual installation:
git clone https://github.com/Syedkashaf2/CODEX.git
cd CODEX
bash install.sh
```

---

## 🚨 Post-Installation Issues

### ❌ Issue: Banner/Prompt Not Showing After Installation

**Cause**: Shell not reloaded or zsh not set as default

**Solution**:
```bash
# 1. Set zsh as default shell
chsh -s zsh

# 2. Exit and reopen Termux

# 3. If still not working, manually load zsh config
exec zsh

# 4. If banner still missing, reload settings
termux-reload-settings
```

---

### ❌ Issue: "command not found: help" or other CODEX commands

**Cause**: Tools not properly linked or PATH not updated

**Solution**:
```bash
# 1. Check if tools exist
ls -la ~/.toolx/

# 2. Check if they're executable
ls -l ~/.toolx/help
ls -l ~/.toolx/chat

# 3. Make sure they're executable
chmod +x ~/.toolx/*

# 4. Reload shell
exec zsh

# 5. Try command again
help
```

---

### ❌ Issue: Font Characters Display as Boxes/Unknown Symbols

**Cause**: Terminal font not installed or not set correctly

**Solution**:
```bash
# 1. Verify font file exists
ls -la ~/.termux/font.ttf

# 2. If missing, reinstall fonts
# Navigate to CODEX directory and run:
cd ~/CODEX
cp files/font.ttf ~/.termux/

# 3. Reload Termux settings
termux-reload-settings

# 4. Close and reopen Termux app
```

---

### ❌ Issue: Colors Look Wrong or Inverted

**Cause**: Color scheme not applied or corrupted

**Solution**:
```bash
# 1. Check if colors.properties exists
ls -la ~/.termux/colors.properties

# 2. If missing, restore it
cd ~/CODEX
cp files/colors.properties ~/.termux/

# 3. Reload settings
termux-reload-settings

# 4. Close and reopen Termux
```

---

### ❌ Issue: Terminal is Very Slow

**Cause**: Too many plugins or heavy theme processing

**Solution**:
```bash
# 1. Edit zshrc and comment out heavy plugins
nano ~/.zshrc

# Find this line:
# plugins=(git)

# 2. Disable auto-update (causes slowdown)
# Add to ~/.zshrc:
DISABLE_AUTO_UPDATE="true"

# 3. Reload
exec zsh

# 4. If still slow, check running processes
ps aux | head -20
```

---

### ❌ Issue: AutoComplete (Tab) Not Working

**Cause**: ZSH plugins not loaded or corrupted

**Solution**:
```bash
# 1. Check if plugins exist
ls ~/.oh-my-zsh/plugins/

# 2. If zsh-autosuggestions missing, reinstall
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ~/.oh-my-zsh/plugins/zsh-autosuggestions

# 3. If zsh-syntax-highlighting missing, reinstall
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
  ~/.oh-my-zsh/plugins/zsh-syntax-highlighting

# 4. Reload
exec zsh
```

---

### ❌ Issue: Aliases Not Working

**Cause**: Aliases not defined in ~/.zshrc or shell not reloaded

**Solution**:
```bash
# 1. Check if aliases are defined
grep "alias ls=" ~/.zshrc

# 2. If they're missing, add them manually to ~/.zshrc:
alias ll="ls -lah"
alias la="ls -la"

# 3. Reload
exec zsh

# 4. Test alias
ll
```

---

### ❌ Issue: Git Commands Not Working

**Cause**: Git not installed or SSH keys not configured

**Solution**:
```bash
# 1. Install git
pkg install git -y

# 2. Configure git
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# 3. Generate SSH key (if needed)
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa

# 4. Add public key to GitHub/GitLab
cat ~/.ssh/id_rsa.pub

# 5. Test connection
ssh -T git@github.com
```

---

### ❌ Issue: Python Commands/Chat Not Working

**Cause**: Python not installed or incorrect version

**Solution**:
```bash
# 1. Install Python
pkg install python -y

# 2. Verify installation
python --version

# 3. If using Python 3 only:
pkg install python3 -y
python3 --version

# 4. Create alias (if needed)
echo "alias python='python3'" >> ~/.zshrc
exec zsh
```

---

## 🚨 Command-Specific Issues

### ❌ Issue: `chat` Command Not Starting

**Cause**: Dependencies missing or internet connection issues

**Solution**:
```bash
# 1. Install required packages
pkg install jq curl ncurses-utils -y

# 2. Check internet connection
curl -I https://github.com

# 3. Run chat command with debug
bash ~/.toolx/chat -v

# 4. If still fails, try direct:
bash ~/CODEX/files/chat
```

---

### ❌ Issue: `bname` Command Crashes

**Cause**: usernames.txt missing or permission issues

**Solution**:
```bash
# 1. Check if file exists
ls -la ~/.termux/usernames.txt

# 2. If missing, create it
mkdir -p ~/.termux
echo "DX-SIMU" > ~/.termux/usernames.txt

# 3. Make zshrc writable
chmod 644 ~/.zshrc

# 4. Try bname again
bname
```

---

### ❌ Issue: `update` Command Fails

**Cause**: Network issues or GitHub unreachable

**Solution**:
```bash
# 1. Check internet
ping github.com

# 2. Try manual update
cd ~/CODEX
git pull origin main

# 3. Or reinstall from scratch
cd ~
rm -rf CODEX
git clone https://github.com/Syedkashaf2/CODEX.git
cd CODEX
bash install.sh
```

---

## 🚨 Advanced Issues

### ❌ Issue: "tput: not found" or Terminal Control Errors

**Cause**: ncurses-utils not installed

**Solution**:
```bash
pkg install ncurses-utils -y
termux-reload-settings
exec zsh
```

---

### ❌ Issue: "lsd: command not found" but ls aliases fail

**Cause**: lsd (modern ls replacement) not installed

**Solution**:
```bash
# 1. Install lsd
pkg install lsd -y

# 2. Verify
lsd --version

# 3. Reload
exec zsh
```

---

### ❌ Issue: Display Glitches or Corrupted Output

**Cause**: Terminal size detection issues or stale terminal session

**Solution**:
```bash
# 1. Reset terminal
reset

# 2. Clear screen
clear

# 3. Force terminal resize
stty rows $(tput lines) cols $(tput cols)

# 4. Reload shell
exec zsh
```

---

### ❌ Issue: Cannot Remove/Uninstall CODEX

**Cause**: Permission issues or incomplete uninstall script

**Solution**:
```bash
# 1. Make unstall script executable
chmod +x ~/.toolx/unstall

# 2. Run it
unstall

# 3. If that fails, manual cleanup:
rm -rf ~/.oh-my-zsh
rm -rf ~/.zshrc ~/.zsh_history
rm -rf ~/.toolx ~/.Codex-simu ~/.CODEX
rm -rf ~/.termux/font.ttf ~/.termux/colors.properties

# 4. Reset shell to bash
chsh -s bash

# 5. Reload
termux-reload-settings
exit
```

---

## 📝 Diagnostic Commands

### Check Installation Status

```bash
# 1. Verify all key files
echo "=== Checking Installation ==="
echo "ZSH Config:" && test -f ~/.zshrc && echo "✓ Found" || echo "✗ Missing"
echo "Oh-My-Zsh:" && test -d ~/.oh-my-zsh && echo "✓ Found" || echo "✗ Missing"
echo "CODEX Tools:" && test -d ~/.toolx && echo "✓ Found" || echo "✗ Missing"
echo "Terminal Config:" && test -d ~/.termux && echo "✓ Found" || echo "✗ Missing"

# 2. Check current shell
echo "Current Shell: $SHELL"

# 3. Check ZSH version
zsh --version

# 4. Check important commands
echo "=== Command Check ==="
for cmd in git python curl jq lsd zsh; do
    command -v $cmd >/dev/null && echo "✓ $cmd" || echo "✗ $cmd missing"
done

# 5. Disk space
df -h $HOME
```

### Clear Cache & Rebuild

```bash
# 1. Clear all temporary files
rm -rf ~/.cache ~/.local/share/cache

# 2. Reload ZSH completely
exec zsh -l

# 3. If still issues, do full reinstall
cd ~
rm -rf CODEX .oh-my-zsh .zshrc .toolx .CODEX
git clone https://github.com/Syedkashaf2/CODEX.git
cd CODEX
bash install.sh
```

---

## 📞 Still Not Working?

If none of the above solutions work:

1. **Collect Debug Info**:
```bash
echo "=== System Info ===" > codex_debug.txt
uname -a >> codex_debug.txt
termux-setup-storage >> codex_debug.txt 2>&1
pkg list-installed >> codex_debug.txt
```

2. **Report Issue**:
   - Visit: https://github.com/Syedkashaf2/CODEX/issues
   - Include the `codex_debug.txt` file
   - Describe what you did and what error you got

3. **Contact Support**:
   - Telegram: https://t.me/KangCodex
   - Include error messages and Termux version

---

## ✅ Quick Fix Summary

| Issue | Quick Fix |
|-------|-----------|
| Commands not found | `exec zsh` |
| Slow terminal | `DISABLE_AUTO_UPDATE="true"` in ~/.zshrc |
| Font issues | `termux-reload-settings` |
| Plugins missing | `bash install.sh` (reinstall) |
| Full disk | `rm -rf ~/Downloads ~/*.bak` |
| Network timeout | `pkg install curl git -y` & retry |
| Shell wrong | `chsh -s zsh` |
| Corrupted install | `unstall` then reinstall |

---

**Last Updated**: 2026-10-03  
**Status**: Comprehensive Termux Support ✅
