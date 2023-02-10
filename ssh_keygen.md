# `ssh-keygen`: OpenSSH authentication key utility
`ssh-keygen` generates, manages and converts authentication keys for `ssh`

----

### Generate a new key
```
$ ssh-keygen -t rsa -b 4096 -f <filename> -C "<comment>" -N "" -q
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

### Verify private key/public key match
Several methods exist, here's my suggestion: read both private (`-ye`) and public (`-e`) keys then compare the outputs. Bonus points if a common format is specified. For instance:
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

### Useful links
- [How to verify host fingerprint in Openssh](https://superuser.com/questions/1246732/how-to-verify-host-fingerprint-in-openssh)

