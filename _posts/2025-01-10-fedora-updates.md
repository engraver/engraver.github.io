---
layout: post
title:  "Preparing Fedora for normal life"
tags: linux fedora 
---

## DNF update

At some point, the following story is relevant for a fresh Fedora install.

The first magic one should perform on the start, is to update the system:
```bash
sudo dnf update
```
And reboot to be sure that everything works on a fresh system. Usefull stuff I always install first:
```bash
sudo dnf install vim mc 
```

## NVidia drivers

First, we need to [add third-party repositories](https://docs.fedoraproject.org/en-US/quick-docs/rpmfusion-setup/):
```bash
sudo dnf install kmodtool akmods mokutil openssl 
sudo kmodgenca -a 
sudo mokutil --import /etc/pki/akmods/certs/public_key.der 
systemctl reboot 
```
see details in the link above what to press in the menu appearing immediately after reboot.

Second, one [installs NVidia drivers](https://rpmfusion.org/Howto/NVIDIA) from RPM Fusion repository:
```bash
sudo dnf install akmod-nvidia 
sudo dnf install xorg-x11-drv-nvidia-cuda 
```

It is a good idea now to freeze versions of drivers not to get in troubles because of updates:
```bash
dnf install python3-dnf-plugin-versionlock
rpm -qa xorg-x11-drv-nvidia* *kmod-nvidia* nvidia-{settings,xconfig,modprobe,persistenced}  >> /etc/dnf/plugins/versionlock.list
```

And the same stuff with the kernel by adding the line `exclude=kernel*` to `/etc/dnf/dnf.conf`.


## X11 instead of Wayland

X11 package is disabled by default in Fedora KDE, so we install it back:
```bash
sudo dnf install plasma-workspace-x11 kwin-x11
```

Then, it should be enabled in SDDM configuration. We need to edit `/etc/sddm.conf`:
```bash
# Control x11/wayland startup
# DisplayServer=wayland
DisplayServer=x11
```

Optionally, it may be needed to select Plasma (X11) desktop in the SDDM greetings window. 

P. S. Still I do not undestand why Insynk does not work with the default Wayland and requires X11 configuration to sync google drive accounts.



## Final polishing

### General

Usefull stuff I always install last:
```bash
sudo dnf install geany gimp inkscape yakuake ipython
sudo dnf install flexiblas-openblas-threads # needed by gimp
sudo dnf install @development-tools
sudo dnf install gitk texlive-scheme-full texstudio 
sudo dnf install hplip hplip-gui # for HP printers
sudo dnf install libxcrypt-compat # for paraview
```

[Snap repos](https://snapcraft.io/docs/installing-snap-on-fedora):
```bash
sudo dnf install snapd
sudo ln -s /var/lib/snapd/snap /snap
sudo snap install obsidian --classic
sudo snap install spotify
sudo snap install mattermost-desktop --classic
sudo snap install krita
```

[Flatpack repos](https://flatpak.org/setup/Fedora):
```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak install com.anydesk.Anydesk
```

Mamba environment:
```bash
sudo dnf install micromamba
```
Here, we should remove default conda channels to keep the community-based channels only using [these instructions](https://mamba.readthedocs.io/en/latest/user_guide/troubleshooting.html#defaults-channels).

Other stuff: keepassxc, obsidian, insynk, onlyoffice, zoom...

```bash
sudo dnf install hplip hplip-gui
```

### Development

```bash
sudo dnf install qt6-qtbase-devel qt6-qttools-devel qt-creator
```

