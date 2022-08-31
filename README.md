# x1-carbon-9th-gen-ubuntu

Minimal tweaks for a 100% good experience with Lenovo ThinkPad X1 Carbon 9th Gen on Ubuntu 20.04

## What works out of the box

Almost everything. The only minor problem is that the sound is so-so from speakers and headphones.

## Getting same audio quality as in Windows

*Note: I use Bose 700 headphones and JBL Xtreme 2 speakers. Maybe you don't need this with other models/brands.*

### 1. Install PipeWire (for Bluetooth audio codecs)

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

### 2. Install PulseEffects (for Dolby audio)

Install PulseEffects (there's a new software called EasyEffects that didn't work for me):
```
sudo apt install pulseeffects
```

Then in the convulter, import the irs files from the repo.

Source: https://www.reddit.com/r/thinkpad/comments/q5pt38/x1_extreme_gen_4_dolby_atmos_setup_for_linux/
