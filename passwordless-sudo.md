# Passwordless sudo

I like passwordless sudo. Here's a one-liner.

`echo "pi ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/010_pi-nopasswd`
