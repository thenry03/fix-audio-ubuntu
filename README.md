# fix-audio-ubuntu

A simple modification to the `necessary-verbs.sh` script that may help in fixing audio issues on some devices on Ubuntu-based distros.

# Context and Compatibility

This script applies "verbs" (pin configuration commands) to the audio chip. It is especially useful for hardware that does not correctly initialize the audio amplifier at boot on Ubuntu-based distros.

Please note that it is not meant as a permanent solution, but rather a temporary fix while the issue is present. Modern Linux Kernels may eventually include native support for your specific hardware.

# Use Recommendation

You may run it normally, but it is recommended to create a service that executes it at boot. The file for said service is included on this repository.

# Step-by-Step Installation

### 1. Prepare the Script

Move the script to your system's binary folder and grant execution permissions:

```bash
sudo cp necessary-verbs-service-version.sh /usr/local/sbin/
sudo chmod +x /usr/local/sbin/necessary-verbs.sh
```

If your audio card is different from the default (hwC0D0), you must change the $CARD_DEVICE variable value within the script file. You may use the following command to find your device ID:

```bash
aplay -l
```
Then, simply copy that value and use your text editor of choice to modify the script.

### 2. Configure the systemd Service

Copy the service file provided in this repository to the systemd configuration folder:

```bash
sudo cp fix-audio.service /etc/systemd/system/
```

### 3. Enable and start

```bash
sudo systemctl daemon-reload
sudo systemctl enable fix-audio.service
sudo reboot
```

# Important Information

### Confirmed working on the following OS:

- **Ubuntu 22.04 LTS** (Working)
- **Pop!_OS 22.04 LTS** (Working)
- **Pop!_OS 24.04** (Working)

### Original Author:

The original `necessary-verbs.sh` script is maintained and distributed by [Joshua Grisham](https://github.com) in his repository for the Galaxy Book series.
