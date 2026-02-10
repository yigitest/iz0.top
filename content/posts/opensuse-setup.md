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
