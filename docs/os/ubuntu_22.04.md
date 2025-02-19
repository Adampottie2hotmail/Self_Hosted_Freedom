# Setting Up Ubuntu 22.04: Complete Guide

## 1. Download Ubuntu 22.04
Ubuntu 22.04 can be downloaded from the official website:

- [Ubuntu 22.04 LTS Download](https://ubuntu.com/download/desktop)

Choose the **Desktop** or **Server** edition based on your needs.

## 2. Create a Bootable USB
To install Ubuntu, you need to create a bootable USB drive. Use one of the following tools:

- **Windows:** [Rufus](https://rufus.ie/)
- **Linux:** `dd` or [Balena Etcher](https://www.balena.io/etcher/)
- **Mac:** [Balena Etcher](https://www.balena.io/etcher/)

### Create a Bootable USB (Linux CLI):
```bash
sudo dd if=~/Downloads/ubuntu-22.04.iso of=/dev/sdX bs=4M status=progress
```
Replace `/dev/sdX` with your actual USB drive.

## 3. Boot from USB
1. Insert the bootable USB drive into your computer.
2. Restart and enter the BIOS/UEFI (`F2`, `F12`, `Del`, or `Esc` depending on your system).
3. Select the USB drive as the primary boot device.
4. Save and exit BIOS.

## 4. Install Ubuntu 22.04
1. Select **"Try Ubuntu"** or **"Install Ubuntu"**.
2. Choose your **Language** and click **Continue**.
3. Select **Keyboard Layout**.
4. Choose **Installation Type**:
   - **Normal Installation** (Recommended for most users).
   - **Minimal Installation** (For a lightweight setup).
5. Select **Download updates while installing Ubuntu**.
6. Choose **Erase disk and install Ubuntu** *(or manual partitioning for advanced users)*.
7. Select **Time Zone** and enter **Username & Password**.
8. Click **Install Now** → **Restart** when prompted.

## 5. Post-Installation Setup
### Update & Upgrade System
```bash
sudo apt update && sudo apt upgrade -y
```

### Install Essential Packages
```bash
sudo apt install -y curl wget git vim htop
```

### Enable Firewall
```bash
sudo ufw enable
sudo ufw allow OpenSSH  # If you plan to use SSH
```

### Set Up Additional Software (Optional)
- **Snap Applications:**
  ```bash
  sudo snap install vlc
  ```
- **Flatpak:**
  ```bash
  sudo apt install flatpak -y
  ```

### Install NVIDIA Drivers (if needed)
```bash
sudo ubuntu-drivers autoinstall
```

## 6. Setting Up Remote Access (SSH)
If you want to access your system remotely:
```bash
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
```
Check your IP with:
```bash
ip a
```
Then connect via SSH from another machine:
```bash
ssh username@your-ip-address
```

## 7. Final Steps
- **Create Backups:** Set up `Timeshift` for system snapshots.
- **Customize UI:** Use `gnome-tweaks` for additional desktop customization.
- **Enjoy Ubuntu 22.04!** 🚀

This guide covers the complete setup process for Ubuntu 22.04 from scratch. Let me know if you need further tweaks!

