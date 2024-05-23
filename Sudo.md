# Sudo

## Change Sudo Password Timeout

`$ sudo visudo`

Find the following line:

`Defaults env_reset`

And change it like below:

`Defaults env_reset, timestamp_timeout=30`

or add the line if it doesn't exist.

## Default Editor for VISUDO

In `/etc/sudoers` add the following line

```sh
# Defaults specification
Defaults editor=/usr/bin/vim
```

[Index](index.md)


