---
author: Kevin Kunkel
pubDatetime: 2022-09-23T04:58:53Z
title: Getting started with Neovim using NvChad
postSlug: nvchad-setup
featured: true
draft: false
tags:
  - configuration
  - docs
ogImage: ""
description: How to use a pretty solid Neovim configuration to start your journey.
---

Blazing fast Neovim config providing solid defaults and a beautiful UI

## Table of contents

## Pre-requisits

* Neovim 0.9.0.
* Nerd Font as your terminal font.
  * Make sure the nerd font you set doesnt end with Mono to prevent small icons.
  * Example : JetbrainsMono Nerd Font and not JetbrainsMono Nerd Font Mono
* Ripgrep is required for grep searching with Telescope (OPTIONAL).
* GCC, Windows users must have mingw installed and set on path.
* Delete old neovim folder (check commands below)

## Installation

```shell
// old content fetching method
 git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1 && nvim
```

You can configure your own social links along with its icons.

![Nvchad](/assets/nvchad.webp)


## Uninstall

```shell
# Linux / Macos (unix)
rm -rf ~/.config/nvim
rm -rf ~/.local/share/nvim

# Windows
rd -r ~\AppData\Local\nvim
rd -r ~\AppData\Local\nvim-data
```