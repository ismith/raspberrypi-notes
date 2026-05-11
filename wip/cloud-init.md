# Cloud Init

## Context

This might be the safest way to do the intial config I want on an rpi, _and_ to add wifi networks post-setup.

<details><summary>Here's the old way, that I'm replacing.</summary></details>
I initially wanted to edit rootfs directly - that gave me access to:
- etc/netplan yaml files for wifi
- boot/firmware/config.txt

Problem is, if I'm doing this config _on the sdcard_ from my mac, I need to use anylinuxfs to mount rootfs, because rootfs is ext4. It's very cool, it seems to work,
and I worry a bit about forgetting to unmount and thus ending up with a corrupt filesystem. I don't think that's what caused my current issues, but it is possible, 
and regardless, it is additional steps to remember and etc.
</details>

By using the cloud-init approach, I'm only needing to edit bootfs, which Just Works out of the box on a Mac. (Vs rootfs, which needs extra steps.)

The [https://www.raspberrypi.com/news/cloud-init-on-raspberry-pi-os/](https://www.raspberrypi.com/news/cloud-init-on-raspberry-pi-os/) is a major guide for this document,
though there is also [the upstream cloud-init documentation](https://docs.cloud-init.io/en/latest/explanation/introduction.html).

## Goals/Questions
- [ ] what do I put on the sdcard for first boot (after using Raspberry Pi Imager)?
- [ ] can I use this on a previously-set-up card to add ssh keys, wifi networks, etc?
- [ ] can I use Raspberry Pi Imager to flash the sdcard _and add this file_, or do I need to do those two separately?
