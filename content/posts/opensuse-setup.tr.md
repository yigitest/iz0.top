---
title: "Opensuse Setup"
date: 2020-09-15T11:30:03+00:00
kategoriler: [living-guide]
etiketler: [linux, opensuse, kilavuz, notlar]
seriler: []
---

# Opensuse kurulumu sonrasi notlar

## Syncthing kurulumu

```bash
sudo zypper install syncthing
sudo systemctl --user enable syncthing
systemctl --user start syncthing
```

GUI: [http://127.0.0.1:8384/](http://127.0.0.1:8384/)


## Fish

bash, prompt vs ayarlamak yerine, hazir gelen ayarlari daha duzgun olan fish bash kullan.

Sistemin default shell'i bash olarak kalacak ama, konsole default profilini fish yapabiliriz:

```bash
sudo zypper install fish

# Konsole -> Settings -> Configure Konsole -> Profiles -> New
# Command: /usr/bin/fish
# Make default
```