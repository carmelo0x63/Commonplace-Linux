# `ssh-keygen`: OpenSSH authentication key utility
`ssh-keygen` generates, manages and converts authentication keys for `ssh`

----

### Generate a new key
```
$ ssh-keygen -t rsa -b 4096 -f "<filename>" -C "<comment>" -N "" -q
```

**NOTE**:
  `-t`: key type, e.g. `rsa`, `ed25519`
  `-b`: number of bits
  `-f`: filename
  `-C`: helpful comment
  `-N`: passphrase
  `-q`: quiet mode

Two files will be generated in the current directory, namely, <filename> and <filename>.pub:
```
-rw-------  1 <user>  <group>   3.3K Feb 10 12:15 <filename>
-rw-r--r--  1 <user>  <group>   750B Feb 10 12:15 <filename>.pub
```

----

### Verify a remote host's key
The typical scenario, one tries to ssh into a remote host and the following message pops up: 
```
The authenticity of host '<ip_address>' can't be established.
ED25519 key fingerprint is SHA256:a1b***Zk9.
```
How can that `a1b***Zk9` fingerprint be validated?</br>
Well, evidently, we need to get support from the remote host admin. What if we are that persons? What are we supposed to do?</br>
`ssh-keygen` comes to the rescue in that we can invoke it with the `-l` ("show fingerprint of specified public key file") option. For instance:
```
$ ssh-keygen -lf /etc/ssh/ssh_host_ed25519_key.pub -E sha256
256 SHA256:a1b***Zk9 <comment> (ED25519)
```

If the two fingerprints match, we rest assured the server we're trying to connect to is the right one.

----

### Verify private key/public key match
1. Method #1</br>
Read both private (`-ye`) and public (`-e`) keys then compare the outputs. Bonus points if a common format is specified. For instance:
- private key:
```
$ ssh-keygen -yef filename -m PEM
-----BEGIN RSA PUBLIC KEY-----
MIIB***
...
-----END RSA PUBLIC KEY-----
```

- public key:
```
$ ssh-keygen -ef filename.pub -m PEM 
-----BEGIN RSA PUBLIC KEY-----
MIIB***
...
-----END RSA PUBLIC KEY-----
```
**NOTE**: to make the task easier, the output can be piped into, say, good old `md5sum`.

2. Method #2</br>
Calculate the fingerprint of both the private and public keys. For instance:
```
$ ssh-keygen -lf <filename>
<bit_size> <hash_algo>:*** <comment+key_type>
```
**NOTE**: by running the commands in sequence the outputs will be aligned, comparing them is immediate.

----

### Generate public key from private key
```
$ ssh-keygen -f ~/.ssh/private.pem -y > ~/.ssh/public.pem
```

----

### SSH and host keys
Host keys are cryptographic keys pairs used to authenticate computers. Typically stored under `/etc/ssh/`, the file names begin with `ssh_host_` and continue with `rsa`, `ecdsa`, and `ed25519` depending on the algorithm used during the generation.
To re-generate these keys, e.g. a VM has been cloed and it's necessary to uniquely identify it, the following two steps are to be taken on a Debian system:
1. remove the old keys, `# rm -f /etc/ssh/ssh_host_*`
2. manually create new ones, `# dpkg-reconfigure openssh-server`

----

### Useful links
- [How to verify host fingerprint in Openssh](https://superuser.com/questions/1246732/how-to-verify-host-fingerprint-in-openssh)
- [Public key cryptography: RSA keys](https://www.thedigitalcatonline.com/blog/2018/04/25/rsa-keys/)
- [What are SSH Host Keys?](https://www.ssh.com/academy/ssh/host-key)

