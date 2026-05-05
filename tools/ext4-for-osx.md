# Ext4 for OS X

Raspberry Pis by default will have two filesystems:
- bootfs, FAT
- rootfs, ext4

By default, MacOS only speaks the former. For reasons [anylinuxfx describes](https://github.com/nohajc/anylinuxfs#introduction), 3rd-party filesystems on a Mac is a hassle.

This document tells you how to get access to that rootfs on an ARM/Apple Silicon Mac (not Intel Mac; not Windows; and if you're using Linux you already have filesystem support).

## One Time Setup

We'll assume you already have [Homebrew](https://brew.sh/) installed.

```bash
brew tap nohajc/anylinuxfs
brew install anylinuxfs

# Optional, but speeds up use by downloading the needed alpine image
anylinuxfs init
```

### Mounting and using your filesystem

The anylinuxfs README and docs/examples.md are fabulous. But the bare minimum you need is:

```bash
# It'll run without sudo ... but without partition labels and filesystem names
sudo anylinuxfs list

# Pick the IDENTIFIER you want (eg, disk0s5) and mount it rw
# Note: the 'mount' subcommand is implicit, so I omitted it
# Optional `-o ro` flag if you want read-only
#
# As you'd expect on a Mac, it'll default to being mounted at /Volumes/$LABEL (in our case, /Volumes/rootfs.)
sudo anylinuxfs /dev/$IDENTIFER

# When you're done with your filesystem, unmount it
sudo anylinuxfs unmount /dev/$IDENTIFIER
```

Note: per anylinuxfs docs:
    It is needed to run mount commands with sudo otherwise we're not allowed direct access to /dev/disk* files. However, the virtual machine itself will in fact run under the regular user who invoked sudo in the first place (i.e. all unnecessary permissions are dropped after the disk is opened)
