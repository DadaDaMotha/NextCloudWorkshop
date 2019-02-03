# Verbindung zum Server mit ssh

Wie z.B. auch bei der Verschlüsselung von Email wird für ssh ein Schlüsselpaar benötigt.
Dieses besteht aus einem **Public Key** und einem **Private Key**.

**SSH erklärt**

<a href="http://www.youtube.com/watch?feature=player_embedded&v=zlv9dI-9g1U
" target="_blank"><img src="http://img.youtube.com/vi/zlv9dI-9g1U/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="480" height="360" border="10" /></a>


## Schlüssel erzeugen

Starte ein Terminal in Linux.

**Mac/Linux**:

```bash
ssh-keygen -t rsa
cd ./.ssh
ls -la

total 20
drwx------  2 luke luke 4096 Aug 13 10:30 .
drwxr-xr-x 74 luke luke 4096 Aug 31 21:59 ..
-rw-------  1 luke luke 1766 Aug 13 10:30 id_rsa
-rw-r--r--  1 luke luke  394 Aug 13 10:30 id_rsa.pub
-rw-r--r--  1 luke luke 3768 Aug 27 10:47 known_hosts
```

Jetzt muss `id_rsa.pub` ins `~/.ssh/authorized_keys` file auf dem Server. Man kann dies
 manuell tun oder mit `ssh-copy-id`.
`ssh-copy-id` installiert den SSH key auf einem Server als authorisierter Schlüssel.

    ssh-copy-id -p 20 -i ~/.ssh/id_rsa.pub user@my.domain.com
    
With `man ssh-copy-id` you can check the documentation.


Test the new key as user `sshuser`:

```bash

# Verbose mode -v on port 20
ssh -vp 20 user@my.domain.com

```
    
The login should now complete without asking for a password. Note, however,
that the command might ask for the passphrase you specified for the key.

## Controlling access settings on the server

You can exclude simple password auth from allowed password authentification methods once auth with 
your public key works.

    sudo vim /etc/ssh/sshd/sshd_config
    
In here, there are settings like
- Port to connect to
- if password auth is allowed
    
Disable password authentification or remove `#` comment:

    PasswordAuthentification no
    
After changing `sshd_config`, run
    
    service ssh restart
    



