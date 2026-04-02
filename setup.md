# 🐉 Shadow Dragon — Hyprland Setup Guide
### EndeavourOS (No DE) · Intel iGPU · Full Custom Desktop

> **Tema:** Dark Navy · Deep Purple · Magenta Accent · Clean & Powerful  
> **Referensi Warna dari Wallpaper:**
> - Background: `#0a0b14` (near black navy)
> - Primary: `#1e1b4b` (deep indigo)
> - Accent 1: `#7c3aed` (violet/purple)
> - Accent 2: `#d946ef` (magenta/fuchsia)
> - Text: `#e2e8f0` (soft white)
> - Subtle: `#334155` (muted slate)

---

## 📋 DAFTAR ISI

1. [Install EndeavourOS (No DE)](#1-install-endeavouros-no-de)
2. [Post-Install: Update & Setup Dasar](#2-post-install-update--setup-dasar)
3. [Install Hyprland & Wayland Stack](#3-install-hyprland--wayland-stack)
4. [Install Semua Komponen Desktop](#4-install-semua-komponen-desktop)
5. [Konfigurasi Hyprland](#5-konfigurasi-hyprland)
6. [Konfigurasi Waybar](#6-konfigurasi-waybar)
7. [Konfigurasi Dunst](#7-konfigurasi-dunst)
8. [Konfigurasi Rofi](#8-konfigurasi-rofi)
9. [Konfigurasi Kitty Terminal](#9-konfigurasi-kitty-terminal)
10. [Konfigurasi SDDM](#10-konfigurasi-sddm)
11. [Konfigurasi Thunar & File Manager](#11-konfigurasi-thunar--file-manager)
12. [Komponen Tambahan (Power, Clipboard, Screenshot)](#12-komponen-tambahan)
13. [GTK & Icon Theme](#13-gtk--icon-theme)
14. [Wallpaper & Swww](#14-wallpaper--swww)
15. [Fonts](#15-fonts)
16. [Final Check & Troubleshooting](#16-final-check--troubleshooting)

---

## 1. Install EndeavourOS (No DE)

### Saat Proses Instalasi:
1. Boot dari USB EndeavourOS
2. Pilih **"Online Installation"**
3. Di halaman **Desktop Environment**, pilih **"No Desktop"** (paling bawah)
4. Lanjutkan instalasi seperti biasa (partisi, user, timezone, dll)
5. Selesai install, reboot — lo akan masuk ke **TTY** (terminal hitam, no GUI)

> ⚠️ Jangan panik saat masuk TTY. Ini normal. Login dengan username & password yang lo buat saat install.

---

## 2. Post-Install: Update & Setup Dasar

Login ke TTY, lalu jalankan perintah berikut satu per satu:

```bash
# Update sistem dulu
sudo pacman -Syu

# Install tools penting
sudo pacman -S git base-devel wget curl neovim

# Install yay (AUR helper) — penting untuk install paket dari AUR
cd /tmp
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd ~

# Verifikasi yay terinstall
yay --version
```

---

## 3. Install Hyprland & Wayland Stack

```bash
# Install Hyprland (versi stable terbaru dari official repo)
sudo pacman -S hyprland

# Wayland essentials
sudo pacman -S \
  wayland \
  wayland-protocols \
  xorg-xwayland \
  xdg-desktop-portal-hyprland \
  xdg-utils \
  qt5-wayland \
  qt6-wayland

# Audio stack (PipeWire — wajib untuk modern desktop)
sudo pacman -S \
  pipewire \
  pipewire-alsa \
  pipewire-pulse \
  pipewire-jack \
  wireplumber \
  pavucontrol

# Polkit (untuk permission dialog)
sudo pacman -S polkit-kde-agent

# Network manager
sudo pacman -S networkmanager network-manager-applet
sudo systemctl enable NetworkManager

# Intel UHD Graphics driver (wajib untuk Intel integrated GPU)
sudo pacman -S mesa intel-media-driver vulkan-intel
```

---

## 4. Install Semua Komponen Desktop

```bash
# === STATUS BAR ===
sudo pacman -S waybar

# === NOTIFICATION DAEMON ===
sudo pacman -S dunst libnotify

# === APP LAUNCHER ===
sudo pacman -S rofi-wayland

# === LOGIN MANAGER ===
sudo pacman -S sddm
sudo systemctl enable sddm

# === TERMINAL ===
sudo pacman -S kitty

# === FILE MANAGER ===
sudo pacman -S thunar thunar-archive-plugin thunar-volman gvfs gvfs-mtp

# === WALLPAPER DAEMON ===
sudo pacman -S swww

# === SCREENSHOT ===
sudo pacman -S grim slurp swappy

# === CLIPBOARD ===
sudo pacman -S wl-clipboard cliphist

# === SCREEN LOCK ===
yay -S hyprlock

# === IDLE DAEMON (auto lock) ===
sudo pacman -S hypridle

# === LOGOUT / POWER MENU ===
yay -S wlogout

# === GTK THEME ENGINE ===
sudo pacman -S nwg-look

# === FONTS ===
sudo pacman -S \
  ttf-jetbrains-mono-nerd \
  ttf-nerd-fonts-symbols \
  noto-fonts \
  noto-fonts-emoji \
  ttf-font-awesome

# === ICON THEME ===
yay -S papirus-icon-theme

# === GTK DARK THEME ===
sudo pacman -S materia-gtk-theme

# === BRIGHTNESS CONTROL (Intel iGPU) ===
sudo pacman -S brightnessctl

# === BLUETOOTH (opsional) ===
sudo pacman -S bluez bluez-utils blueman
sudo systemctl enable bluetooth

# === IMAGE VIEWER ===
sudo pacman -S imv

# === MEDIA PLAYER ===
sudo pacman -S mpv

# === SYSTEM MONITOR ===
sudo pacman -S btop

# === APP PORTAL (untuk file picker di browser, dll) ===
sudo pacman -S xdg-desktop-portal-gtk
```

---

## 5. Konfigurasi Hyprland

Buat direktori konfigurasi:

```bash
mkdir -p ~/.config/hypr
nvim ~/.config/hypr/hyprland.conf
```

---

## 6. Konfigurasi Waybar

```bash
mkdir -p ~/.config/waybar
```

### `~/.config/waybar/config.jsonc`

```bash
nvim ~/.config/waybar/config.jsonc
```

### `~/.config/waybar/style.css`

```bash
nvim ~/.config/waybar/style.css
```

---

## 7. Konfigurasi Dunst

```bash
mkdir -p ~/.config/dunst
nvim ~/.config/dunst/dunstrc
```

---

## 8. Konfigurasi Rofi

```bash
mkdir -p ~/.config/rofi
nvim ~/.config/rofi/config.rasi
```


```bash
nvim ~/.config/rofi/shadow-dragon.rasi
```

---

## 9. Konfigurasi Kitty Terminal

```bash
mkdir -p ~/.config/kitty
nvim ~/.config/kitty/kitty.conf
```

---

## 10. Konfigurasi SDDM

```bash
# Install tema SDDM
yay -S sddm-theme-corners-git

# Buat direktori config
sudo mkdir -p /etc/sddm.conf.d
sudo nvim /etc/sddm.conf.d/10-hyprland.conf
```

```ini
[Autologin]
# Hapus tanda # dan isi username lo kalau mau auto-login
# User=yourusername
# Session=hyprland

[Theme]
Current=corners

[General]
HaltCommand=/usr/bin/systemctl poweroff
RebootCommand=/usr/bin/systemctl reboot

[Wayland]
CompositorCommand=kwin_wayland --drm --no-lockscreen
```

> 💡 **Tips:** Kalau lo mau tampilan SDDM tetap simpel, bisa juga pakai tema `sugar-dark`:
> ```bash
> yay -S sddm-sugar-dark
> ```
> Lalu ganti `Current=corners` → `Current=sugar-dark`

---

## 11. Konfigurasi Thunar & File Manager

```bash
# Pastikan semua sudah terinstall
sudo pacman -S thunar gvfs gvfs-mtp tumbler ffmpegthumbnailer

# Buka Thunar dan set preferences via GUI (tampil otomatis saat launch)
# Atau set via terminal:
xfconf-query -c thunar -p /misc-show-delete-action -s true
```

**Fitur Thunar yang diaktifkan:**
- Custom Actions (klik kanan → Open Terminal Here)

```bash
# Tambah custom action "Open Terminal Here":
# Thunar → Edit → Configure Custom Actions → Add
# Name: Open Terminal
# Command: kitty --working-directory %f
# Icon: utilities-terminal
# File Pattern: *
# Appears if selection contains: Directories
```

---

## 12. Komponen Tambahan

### Hyprlock (Screen Locker)

```bash
mkdir -p ~/.config/hypr
nvim ~/.config/hypr/hyprlock.conf
```

### Hypridle (Auto Lock)

```bash
nvim ~/.config/hypr/hypridle.conf
```

### Wlogout (Power Menu)

```bash
mkdir -p ~/.config/wlogout
nvim ~/.config/wlogout/layout
```

```bash
nvim ~/.config/wlogout/style.css
```

---

## 13. GTK & Icon Theme

```bash
mkdir -p ~/.config/gtk-3.0 ~/.config/gtk-4.0

# GTK 3
nvim ~/.config/gtk-3.0/settings.ini
```

```bash
# GTK 4
nvim ~/.config/gtk-4.0/settings.ini
```

```bash
# Install cursor tema
yay -S bibata-cursor-theme

# Set cursor via nwg-look (GUI)
nwg-look

# Atau manual
mkdir -p ~/.icons/default
nvim ~/.icons/default/index.theme
```

```ini
[Icon Theme]
Name=Default
Comment=Default Cursor Theme
Inherits=Bibata-Modern-Classic
```

---

## 14. Wallpaper & Swww

```bash
# Buat folder wallpaper
mkdir -p ~/Pictures/Wallpapers

# Copy wallpaper lo ke sana
cp /path/to/wallpaper.jpg ~/Pictures/Wallpapers/wallpaper.jpg

# Test swww (jalankan setelah masuk Hyprland):
swww-daemon &
swww img ~/Pictures/Wallpapers/wallpaper.jpg \
  --transition-type wipe \
  --transition-fps 60 \
  --transition-duration 1.5
```

---

## 15. Fonts

```bash
# Rebuild font cache setelah install semua font
fc-cache -fv

# Verifikasi JetBrainsMono tersedia
fc-list | grep -i jetbrains
```

---

## 16. Final Check & Troubleshooting

### Masuk ke Hyprland Pertama Kali

Setelah semua config selesai, **reboot** sistem:

```bash
sudo reboot
```

SDDM akan muncul. Login, dan Hyprland akan start otomatis.

### Jika Hyprland Crash / Tidak Start

Boot ke TTY (Ctrl+Alt+F2), lalu cek log:

```bash
# Cek error log Hyprland
cat ~/.local/share/hyprland/hyprland.log | tail -50

# Atau jalankan Hyprland manual dari TTY untuk lihat error langsung:
Hyprland
```

### Cek Semua Service

```bash
# Cek PipeWire
systemctl --user status pipewire pipewire-pulse wireplumber

# Restart jika perlu
systemctl --user restart pipewire pipewire-pulse wireplumber

# Cek NetworkManager
systemctl status NetworkManager
```

### Waybar Tidak Muncul

```bash
# Test waybar manual dari terminal (Mod+Return untuk buka kitty)
waybar &

# Lihat error
waybar 2>&1 | head -30
```

### Screen Tearing (Intel iGPU)

Buat file:

```bash
sudo nvim /etc/environment
```

Tambahkan:
```
LIBVA_DRIVER_NAME=iHD
```

### Aplikasi Tidak Bisa Buka File (Portal Error)

```bash
# Pastikan xdg-desktop-portal jalan
systemctl --user status xdg-desktop-portal
systemctl --user status xdg-desktop-portal-hyprland

# Restart jika error
systemctl --user restart xdg-desktop-portal xdg-desktop-portal-hyprland xdg-desktop-portal-gtk
```

---

## ⌨️ CHEAT SHEET KEYBINDING

| Shortcut | Action |
|---|---|
| `Super + Enter` | Buka terminal (Kitty) |
| `Super + Shift + Enter` | App launcher (Rofi) |
| `Super + E` | File manager (Thunar) |
| `Super + B` | Browser (Firefox) |
| `Super + Q` | Tutup window |
| `Super + F` | Fullscreen |
| `Super + Shift + F` | Toggle float |
| `Super + H/J/K/L` | Pindah fokus (vim) |
| `Super + Shift + H/J/K/L` | Pindah window |
| `Super + Alt + H/J/K/L` | Resize window |
| `Super + 1-0` | Switch workspace |
| `Super + Shift + 1-0` | Move window ke workspace |
| `Super + S` | Scratchpad toggle |
| `Super + V` | Clipboard history |
| `Super + Shift + L` | Lock screen |
| `Super + Shift + Q` | Power menu |
| `Print` | Screenshot area |
| `Super + Print` | Screenshot fullscreen |
| `Super + Shift + S` | Screenshot → clipboard |

---

> 🐉 **Shadow Dragon Desktop** — Built with EndeavourOS + Hyprland  
> Designed for power, elegance, and speed.
