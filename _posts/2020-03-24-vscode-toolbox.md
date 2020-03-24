---
layout: post
title: Integrating Fedora Toolbox into VS Code (with the help of SSH)
---

[VS Code][code] has become my favourite editor as of late, however, using it out of a Flatpak environment on Fedora Silverblue is limited. You can [configure][flatpak-spawn] the built-in terminal to run in Toolbox, but that doesn’t help if extensions need tooling installed.

Copying the approach of [CLion and WSL][clion-wsl], this is a straight-forward how-to for container-based development in VS Code.

First, [create][toolbox] a toolbox.

```text
$ toolbox enter
$ sudo dnf install openssh-server
```

On a regular Fedora system, launching `sshd` with `systemctl` would trigger `sshd-keygen.target`. We can’t do this in Toolbox, so we have to do it manually.

```text
$ sudo /usr/libexec/openssh/sshd-keygen rsa
$ sudo /usr/libexec/openssh/sshd-keygen ecdsa
$ sudo /usr/libexec/openssh/sshd-keygen ed25519
```

Inside `/etc/ssh/sshd_config`, ensure these options are set:

```text
Port 2222                 # Prevent conflicts with other SSH servers
ListenAddress localhost   # Don’t allow remote connections
PermitEmptyPasswords yes  # Containers lack passwords by default
```

NB: Due to container limitations, interactive sessions [won’t work][source].

Exit the toolbox. You can now run the server with a `toolbox run sudo /usr/sbin/sshd`. You can add this into your `.bashrc` if you want it to run automatically.

Add this to your `~/.ssh/config`:

```text
Host toolbox
    HostName localhost
    Port 2222
```

Inside VS Code, install the ‘[Remote – SSH][remote]’ extension, initialise a connection and pick ‘toolbox’ as the host, and enjoy.

[code]: https://flathub.org/apps/details/com.visualstudio.code
[flatpak-spawn]: https://discussion.fedoraproject.org/t/developing-applications-using-flatpak-packaged-editors-ides/269/19
[toolbox]: https://docs.fedoraproject.org/en-US/fedora-silverblue/toolbox/#toolbox-first-toolbox
[clion-wsl]: https://github.com/JetBrains/clion-wsl
[source]: https://discussion.fedoraproject.org/t/ssh-into-a-toolbox/2155/12
[remote]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh
