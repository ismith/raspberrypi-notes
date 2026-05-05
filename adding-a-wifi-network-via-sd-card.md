# Adding a WiFi network via sd card

It's a bit hacky, but the easiest way to add a new WiFi network to an rpi whose known networks are elsewhere might be just editing the sd card from your laptop.

First, if you're on a Mac, check out [tools/ext4-for-osx.md](tools/ext4-for-osx.md).

The partition you want is `rootfs`. At least as of Debian Trixie, on an rpi set up with Raspberry Pi Installer, wifi config is done in yamls in `etc/netplan`, which gets rendered at boot time into NetworkManager connection files. Those yamls are probably root-only.

One of those yamls will have `network.wifis.wlan0`; `wlan0` is the network interface. Under `wlan0` is an `accesspoints` map.

For me, mine had (with different indentation, match what's in your file):
```
access-points:
  "Free Astound WiFi":
    networkmanager:
      uuid: "66d6b63d-8075-35af-b33a-20dff2a7895b"
      name: "netplan-wlan0-Free Astound WiFi"
      passthrough:
        proxy._: ""
```

"Free Astound WiFi" is an open, no-password network; just add your new network below it:
access-points:
  "Free Astound WiFi":
    networkmanager:
      uuid: "66d6b63d-8075-35af-b33a-20dff2a7895b"
      name: "netplan-wlan0-Free Astound WiFi"
      passthrough:
        proxy._: ""
  "YourNewSSID":
    password: "YourNewPassword"
```

You don't need the `networkmanager:` bit, including the passthrough/proxy stuff. You can leave old networks (SSIDs) in place or remove them if you no longer need that network and password.
