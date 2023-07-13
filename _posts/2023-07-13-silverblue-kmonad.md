---
title: "Installing KMonad on Fedora Silverblue"
layout: post
---

Since KMonad does not have a Fedora package, I was reluctant to try it out. However, it is much simpler than I thought, although it does have a few quirks, so I decided to write a short guide.

## Installation

I used the [`stack`][stack] for this, but you might prefer to use [Docker][docker] instead.

```bash
git clone git@github.com:kmonad/kmonad.git
cd kmonad
toolbox create kmonad
toolbox enter kmonad
sudo dnf install stack
stack install
```

This will install KMonad into `~/.local/bin`. It does not need to be installed system-wide.

## Permissions

To run KMonad, you will also need to configure some [necessary permissions][permissions].

First, add the udev rule for UInput, e.g. in `/etc/udev/rules.d/90-kmonad.rules`:

```
KERNEL=="uinput", MODE="0660", GROUP="uinput", OPTIONS+="static_node=uinput"
```

A [Silverblue-specific workaround][groups] is needed to be able to add the user to the required groups.

```bash
grep -E '^uinput:' /usr/lib/group >> /etc/group
grep -E '^input:' /usr/lib/group >> /etc/group
systemctl reboot
```

Then, add the user to the `uinput` and `input` groups:

```bash
sudo usermod -aG uinput $USER
sudo usermod -aG input $USER
```

Log out and log back in, and you should be able to run `kmonad`.

## Autostarting

There is a [systemd service][startup] available in the repo.

If you want an easier way to control it, I wrote an [extension][extension] for integrating it into GNOME Shell.

[<img src="https://raw.githubusercontent.com/andyholmes/gnome-shell-extensions-badge/master/get-it-on-ego.svg?sanitize=true" alt="Get it on GNOME Extensions" height="100">][extension]


[stack]: https://github.com/kmonad/kmonad/blob/master/doc/installation.md#using-stack
[docker]: https://github.com/kmonad/kmonad/blob/master/doc/installation.md#using-docker
[permissions]: https://github.com/kmonad/kmonad/blob/master/doc/faq.md#q-how-do-i-get-uinput-permissions
[groups]: https://docs.fedoraproject.org/en-US/fedora-silverblue/troubleshooting/#_unable_to_add_user_to_group
[startup]: https://github.com/kmonad/kmonad/tree/master#startup
[extension]: https://extensions.gnome.org/extension/6069/kmonad-toggle/
