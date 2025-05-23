# journal-vsock-export

A simple systemd service which exports journal messages from a VM to 
the host over VSOCK.

It exports all journal messages of the current boot.

See https://github.com/adombeck/journal-vsock-sink for the counterpart
on the host which receives the messages and stores them in `/var/log/journal/vsock`.

Note that systemd v256 has built-in support to forward journal messages 
via VSOCK, so instead of using journal-vsock-export, you can add

```
ForwardToSocket=vsock:2:52000
```

to `/etc/systemd/journald.conf`. Note that this misses a large part of
the messages produced during boot, because it only starts forwarding
after the journald service has started and the network is ready.

## Installation

1. Clone the repository
2. Run `sudo ./install.sh`
