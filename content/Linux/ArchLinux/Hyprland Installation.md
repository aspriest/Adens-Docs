# Hyprland Installation

[Hyprland Installation Guide](https://wiki.hyprland.org/Getting-Started/Installation/)

## Notes:

- When trying to use cmake I found it was not installed. I then tried to install with `sudo pacman -S cmake`. This gave an error. I then tried running `sudo pacman -Syu` updating pacman. This fixed the issue and was able to install cmake.
- I had to install gtk3 to ensure Hyprland operated correctly.

## SDDM

Installed sddm via pacman and enabled using systemctl.

I then wanted to change the theme. I opted to use a pre-configured one from here: https://github.com/Keyitdev/sddm-astronaut-theme/blob/master/README.md

I tried using the manual installation but failed. I think it was because I didn't restart the sddm service. But before i tried that I just used the provided shell script in the readme.
