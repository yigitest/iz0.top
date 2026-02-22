---
title: "Opensuse Setup"
date: 2020-09-15T11:30:03+00:00
categories: [living-guide]
tags: [linux, opensuse, guide, notes]
series: []
kategoriler: [yasayan-kilavuz]
etiketler: [linux, opensuse, kilavuz, notlar]
seriler: []
---

## Notes after Opensuse installation

### Flatpaks

[opensuse.org/Flatpak](https://en.opensuse.org/Flatpak#System_Level_Setup)

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

flatpak update
```

#### automatic update services

```bash
sudo systemctl edit --full --force flatpak-system-update.service
```

```
[Unit]
Description=Flatpak Automatic Update
Documentation=man:flatpak(1)
Wants=network-online.target
After=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/bin/flatpak --system uninstall --unused -y --noninteractive ; /usr/bin/flatpak --system update -y --noninteractive ; /usr/bin/flatpak --system repair
```

```bash
sudo systemctl edit --full --force flatpak-system-update.timer
```

```
[Unit]
Description=Flatpak Automatic Update Trigger
Documentation=man:flatpak(1)

[Timer]
RandomizedDelaySec=10m
OnBootSec=2m
OnCalendar=*-*-* 4:00:00
Persistent=true

[Install]
WantedBy=timers.target
```

```bash
sudo systemctl daemon-reload && sudo systemctl enable --now flatpak-system-update.timer
```

### Syncthing installation

```bash
sudo zypper install syncthing
sudo systemctl --user enable syncthing
systemctl --user start syncthing
```

GUI: [http://127.0.0.1:8384/](http://127.0.0.1:8384/)

### Fish

Instead of setting up bash and prompt, use fish shell, which comes with better default settings.

The system's default shell will remain bash, but you can set the default profile in Konsole to fish:

```bash
sudo zypper install fish

# Konsole -> Settings -> Configure Konsole -> Profiles -> New
# Command: /usr/bin/fish
# Make default
```

### Use oci for codec installation

```
sudo zypper install opi
opi codecs
```

### /etc/hosts

Add computer's hostname to /etc/hosts file. 

```
hostnamectl

>> Static hostname: thinkpad1235u

sudo nano /etc/hosts

>> 127.0.0.1 thinkpad1235u
```

[https://bugzilla.opensuse.org/show_bug.cgi?id=1214043#c9](https://bugzilla.opensuse.org/show_bug.cgi?id=1214043#c9)