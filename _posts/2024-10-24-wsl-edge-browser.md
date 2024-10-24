---
title: 'WSL should use the MS Edge browser for aws sso'
date: 2024-10-24
categories: [IT]
tags: [sso, edge, aws, login]
---
I've installed chromium within my wsl without any desktop environment etc.  
When I start an aws sso login the chromium will open, but it looks kind of weired,  
so why don't use the Microsoft Edge Browser on the host system.  
```
sudo ln -s /mnt/c/Program\ Files\ \(x86\)/Microsoft/Edge/Application/msedge.exe /usr/bin/msedge
sudo update-alternatives --install /usr/bin/x-www-browser x-www-browser /usr/bin/msedge 100
sudo update-alternatives --config x-www-browser
```
