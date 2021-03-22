---
layout: post
title: Integrating Fedora Toolbox into VS Code (with the help of SSH)
---

[VS Code][code] has become my favourite editor as of late, however, using it out of a Flatpak environment on Fedora Silverblue is limited. You can [configure][flatpak-spawn] the built-in terminal to run in Toolbox, but that doesn’t help if extensions need tooling installed.

Copying the approach of [CLion and WSL][clion-wsl], this is a straight-forward how-to for container-based development in VS Code.

First, [create and enter][toolbox] a toolbox. Once inside, we need to install and configure the SSH server.

```text
⬢[user@toolbox ~]$ sudo dnf install openssh-server
```

On a regular Fedora system, launching `sshd` with `systemctl` would trigger `sshd-keygen.target`. We can’t do this in Toolbox, so we have to do it manually.

```text
⬢[user@toolbox ~]$ sudo /usr/libexec/openssh/sshd-keygen rsa
⬢[user@toolbox ~]$ sudo /usr/libexec/openssh/sshd-keygen ecdsa
⬢[user@toolbox ~]$ sudo /usr/libexec/openssh/sshd-keygen ed25519
```

Inside `/etc/ssh/sshd_config`, ensure these options are set (assuming you are running Fedora 33 inside):

```text
# For VS Code
Port 2233                 # Prevent conflicts with other SSH servers
ListenAddress localhost   # Don’t allow remote connections
PermitEmptyPasswords yes  # Containers lack passwords by default
PermitUserEnvironment yes # Allow setting DISPLAY for remote connections
```

I like including the Fedora version in the container in the port so that I can have multiple versions at the same time and don’t have to remove lines in `~/.ssh/known_hosts` on container upgrades.

NB: Due to container limitations, interactive sessions [won’t work][source].

Exit the toolbox. You can now run the server with a `toolbox run sudo /usr/sbin/sshd`. You can add this into your `.bash_profile` if you want it to run automatically.

Add this to your `~/.ssh/config`:

```text
Host toolbox-33
    HostName localhost
    Port 2233
```

And this to `~/.ssh/environment` (this allows to starts Xorg apps from VS Code):
```text
DISPLAY=:0
```

Inside VS Code, install the ‘[Remote – SSH][remote]’ extension, initialise a connection and pick ‘toolbox-33’ as the host, and enjoy.

[**Bonus tip**][symlinks]: Open your projects via `/var/home/…` instead of
`/home/…` to avoid symlink bugs.

[code]: https://flathub.org/apps/details/com.visualstudio.code
[flatpak-spawn]: https://discussion.fedoraproject.org/t/developing-applications-using-flatpak-packaged-editors-ides/269/19
[toolbox]: https://docs.fedoraproject.org/en-US/fedora-silverblue/toolbox/#toolbox-first-toolbox
[clion-wsl]: https://github.com/JetBrains/clion-wsl
[source]: https://discussion.fedoraproject.org/t/ssh-into-a-toolbox/2155/12
[remote]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh
[symlinks]: https://discussion.fedoraproject.org/t/tip-use-var-home-instead-of-home-in-vs-code/21887
