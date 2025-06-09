### General commands

#### Connect to <host> over SSH on custom port 2222 (default port is 22)
`ssh -p 2222 <user1>@<host1>`

#### Use SSH key authentication instead of password authentication 
`ssh -i /path/to/private-key <user1>@<host1>`

#### Prevent SSH connection timeout due to prolonged inactivity 
`ssh -o ServerAlivelnterval=60 <user1>@<host1>`

#### Prevent the host key to be saved locally
`ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null <user1>@<host1>`

#### Run a non-interactive command on a remote host directly over SSH
`ssh <user1>@<host1> "ls -Al"`

#### Copy the user's public key to <host> for SSH key authentication 
`ssh-copy-id -i /path/to/public-key <user1>@<host1>`

#### Connect to <host> with custom options defined in SSH config file 
`ssh -F /path/to/ssh_config <user1>@<host1>`

#### Create a SOCKS proxy on local port <port1> with compression enabled
`ssh -D <port1> -C <user1>@<host1>`

----

### Forwarding

[Client]---[host1]---[host2]

#### Start an SSH tunnel then immediately go to background
`ssh -NfL <local-port>:localhost:<port1> <user1>@<host1>`

#### Forward traffic on <local-port> to <host1>:<port> via jump server at <host2>
`ssh -L <local-port>:<host1>:<port1> <user1>@<host2>`

#### Connect to <host2> via an intermediate jump server at <host1>:<port1>
`ssh -J <user1>@<host1>:<port1> <user2>@<host2>`

#### Forward traffic on port <remote-port> of <host> to port 22 of local server
`ssh -fN -R <remote-port>:localhost:22 <user1>@<host1>`

https://iximiuz.com/en/posts/ssh-tunnels/
https://docs.ces.cisco.com/docs/cli-instructions-connect2cessh-linuxos-x-users

----

### Transfer local dir to remote path hosted at <host1> on custom SSH port 2222
`scp -rP 2222 /path/to/local-dir <user1>@<host1>:/path/to/remote-dir`
