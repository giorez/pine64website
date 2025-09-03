---
title: "Security"
draft: false
menu:
  docs:
    title:
    parent: "PinePhone/Software_tricks"
    identifier: "PinePhone/Software_tricks/Security"
    weight: 1
aliases:
  - /wiki/PinePhone_Security
---

{{% docs/construction %}}

## Encryption

While encryption alone is not sufficient to protect sensitive data, it is an important tool to safeguard data in certain attack vectors.

### Full-Disk Encryption

Full-disk encryption encrypts the entire disk (except for the boot bits). Currently some operating systems such as postmarketOS and Mobian offer an installation image, which have the option to encrypt the entire disk. Some operating systems, such as postmarketOS (via pmbootstrap) and Arch Arm also offer an installation script for an fully encrypted installation.

Decryption is done at boot after entering the encryption password via an on-screen keyboard (Osk-sdl).

### Encrypted home directory

## SSH

An open SSH port is a typical gateway for attackers on any device exposed to the public Internet. Exposed devices might be attacked within minutes after being exposed. Typically such attacks try default passwords such as "12345", potentially putting the user at risk after connecting the phone to an open/unsecured access point, activating mobile data or mobile Internet.

For safety reasons it is highly recommended to only use SSH in combination with keys, instead of simple numeric passwords.

To generate a key pair for ssh, open a terminal on your local computer, and type

    ssh-keygen

It will ask you where to save the key pair. By default, this is in ~./ssh . Usually it’s best to keep it in the default location. If you have previously generated a key pair, it will ask you if you wish to overwrite your existing one. You probably do not want to do this, as you will no longer be able to use your existing key pair for authentication.

Next, you will be prompted to enter a passphrase. It is recommended that you use this feature.

{{< admonition type="note" >}}
 Do not share your private key with anyone, nor change its file permissions
{{</ admonition >}}

Now, you must start SSHD on your distribution of choice, as this process varies depending on init system, please consult the documentation of your distribution.

Now enabled, you can copy over your public key either manually, or via

    ssh-copy-id $username@$ipaddress

replacing the variables "$username" and "$ipaddress" with the appropriate values, e.g user@192.168.1.15

You may see a message similar to this

    Output
    The authenticity of host '192.168.1.15 (192.168.1.15)' can't be established.
    ECDSA key fingerprint is fd:fd:d4:f9:57:fe:23:44:e1:55:00:bd:d6:6d:42:fe.
    Are you sure you want to continue connecting (yes/no)?

This will happen anytime you connect to a new host. Type "yes" and hit enter.

finally, to disable password authentication, type

    sed -i -E 's/#?PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config

as root on your PinePhone and either restart the sshd service, or reboot your device
