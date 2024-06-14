# Mac OS: How to Configure Touch ID for the `sudo` command

Touch ID can be used on Mac as a convenient way to authenticate without typing in your password. This is also possible in the terminal, especially for `sudo` commands.

To allow Touch ID on your Mac for sudo access instead of using a password, you need to edit the `pam.d` configuration files.

As root, edit `/etc/pam.d/sudo` and add at the top of the file the following line: 

`auth       sufficient     pam_tid.so`

The contents of this file should look like this:

```shell
# sudo: auth account password session
auth       sufficient     pam_tid.so
auth       sufficient     pam_smartcard.so
auth       required       pam_opendirectory.so
account    required       pam_permit.so
password   required       pam_deny.so
session    required       pam_permit.so
```

If you then use `sudo` in the terminal, you should be prompted to authenticate with Touch ID.

**Source: https://apple.stackexchange.com/a/306324/409134**