## Setup ssh client in Ubuntu 

```bash
# Create key if needed or skip and copy your key to ~/.ssh/id_rsa, if existed
$ ssh-keygen -t rsa -b 4096 -C "your_mail@your_domain"

# Ssh-agent: add next two lines to ~/.bashrc
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_rsa

$ source ~/.bashrc

# Go to github and paste contents of ~/.id_rsa.pub there https://github.com/settings/ssh/new

# Test key on github
Check out the [](linux/ssh-goodies) section for further information.
$ ssh -T git@github.com

# Change passphrase if desired: 
$ ssh-keygen -p
```

Write in ~/.ssh/config, for example:
```
Host me
  Hostname myhost
  Port 2222
  User username
  IdentityFile ~/.ssh/id_rsa
```

```bash
# Protect ssh files
$ chmod -R o-rwx,g-rwx ~/.ssh/*
# Copy public key to server
$ ssh-copy-id -i ~/.ssh/id_rsa.pub me
```
