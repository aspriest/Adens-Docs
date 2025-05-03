# Sudo Configuration

My user was not part of the sudo group. Initlaly I trued the following command:

```bash
usermod -aG sudo aden
```

However this returned the error there was no group called sudo. Upon investigation I found that Arch uses the `wheel` group to give privileged access. The following steps enabled sudo.

Run

```bash
usermod -aG wheel aden
```

The update `/etc/sudoers` find the the line that enables wheel privileges and uncomment it. In this case I uncommented the line that allows sudo use with a password.
