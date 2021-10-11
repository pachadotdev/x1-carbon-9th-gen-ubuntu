# x1-carbon-9th-gen-ubuntu

Minimal tweaks for a 100% good experience with Lenovo ThinkPad X1 Carbon 9th Gen on Ubuntu 20.04

## What works out of the box

Almost everything. The only minor problem is that the sound is so-so from speakers and headphones.

## Getting same audio quality as in Windows

*Note: I use Bose 700 headphones and JBL Xtreme 2 speakers. Maybe you don't need this with other models/brands.*

### 1. Install PipeWire

Install PipeWire and also mask PulseAudio:
```
sudo add-apt-repository ppa:pipewire-debian/pipewire-upstream
sudo apt update
sudo apt install pipewire
sudo apt install libspa-0.2-bluetooth
sudo apt install pipewire-audio-client-libraries
systemctl --user daemon-reload
systemctl --user --now disable pulseaudio.service pulseaudio.socket
systemctl --user mask pulseaudio
systemctl --user --now enable pipewire-media-session.service
```

Then reboot and type
```
pactl info
```

It should display
```
Server Name: PulseAudio (on PipeWire 0.3.38)
Server Version: 15.0.0
```

This provides AAC and SBC codes for high quality bluetooth audio.

Source: Adapted from https://askubuntu.com/questions/1339765/replacing-pulseaudio-with-pipewire-in-ubuntu-20-04

### 2. Install PulseAudio volume control

Install with:
```
sudo apt install pavucontrol
```

Then pin the PulseAudio volume control to the side bar, it fixes a Gnome audio bug that doesn't change the output audio device, and it also allows to send different apps to different audio outputs.
