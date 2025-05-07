# Audio Configuration

## Linux Sound Systems and Servers

A sound server is software that manages the use of and access to audio devices, usually a sound card. It commonly runs as a background process or daemons. 

Audio apps make use of a sound server API to access the sound card drivers, and this is the reason why there are dependencies between them.

The layers on a sound server, from a top down perspective, are:

1. Application
2. Sound  (e.g. PipeWire)
3. Sound System
4. Operating System

### Sound Systems

Sound systems provide an API to communicate to sound drivers. Unlike the sound servers they are part of the Linux kernel.

### Sound Servers

Sound servers rely on a sounds system to communicate to the sound drivers.

## PipeWire

PipeWire is an audio service for Linux. It is a framework that works with different kinds of multimedia data (sound, video and MIDI). It allows you to connect different software and hardware devices. Moreover PipeWire has been integrated with Wayland, which is the compositor I currently use on my Arch system.

PipeWire is a newer alternative to PulseAudio.


### Installation

1. Install PipeWire with pacman.

```bash
sudo pacman -S pipewire, pipewire-pulse
```

*note: pipewire-pulse is a component of PipeWire that acts as a compatibility layer for applications designed to work with PulseAudio.*

2. Install a session manager.

```bash
sudo pacman -S wireplumber
```
3. Enable and start the pipewire, pipewire-pulse and wireplumber services.

```bash
systemctl --user --now enable pipewire pipewire-pulse wireplumber
```

4. Disable PulseAudio servers

```bash
systemctl --user --now disable pulseaudio
```

5. Remove PulseAudio to prevent conflicts with PipeWire

```bash
sudo pacman -Rns pulseaudio
```

You can check what Sound server you have running by running:

```bash
pactl info
```
**note: pacttl is CLI tool for controlling a running PulseAudio sever. **

example output:
```bash
Server String: /run/user/1000/pulse/native
Library Protocol Version: 35
Server Protocol Version: 35
Is Local: yes
Client Index: 89
Tile Size: 65472
User Name: aden
Host Name: archlinux
Server Name: PulseAudio (on PipeWire 1.4.2)
Server Version: 15.0.0
Default Sample Specification: float32le 2ch 48000Hz
Default Channel Map: front-left,front-right
Default Sink: alsa_output.pci-0000_00_1b.0.analog-stereo
Default Source: alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
```
---

#### Sources
https://linuxgenie.net/install-pipewire-on-arch-linux/
https://runmodule.com/2021/12/11/linux-sound-servers/