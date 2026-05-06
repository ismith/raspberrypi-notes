# SSH Public Keys

For ease of use, I like to add ssh keys to my pis.

Raspberry Pi Installer offers this on setup, but if you already have password access and want to add your local key:
`ssh-copy-id pi@$HOSTNAME`.

Or, to install all of a github user's pubkeys:
`ssh-import-id-gh $GITHUB_USER`.

(This is a wrapper for `curl https://github.com/$USERNAME.keys >> ~/.ssh/authorized_keys`. `-gl` and `-lh` are also supported for GitLab and Launchpad, respectively.)

## PasswordAuthentication
Password auth is less secure ... but on a shared resource, in some contexts, it may be useful to keep as an option.

Edit `/etc/ssh/sshd_config`, changing `PasswordAuthentication no` to `yes` (or vice versa).

You may also need to check `/etc/ssh/sshd_config.d/50-cloud-init.conf`, Raspberry Pi Installer likes to put stuff there.
