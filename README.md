# xferlogd
Xfer log processing and automation daemon

This tool will let you send pushbullet notifications when someone download a file on your FTP.
You can fork this project to add support for other notification systems (ie, slack, Mattermost, Pushover, ...). The code is very simple and modular, so adding a new system shouldn't be very difficult.

## Prerequisites

Install the following perl modules:
- File::Basename
- Sys::Syslog
- File::Read
- TOML
- Number::Bytes::Human

## Installation

1. Copy configuration `xferlogd.conf` file in `/etc/xferlogd.conf` and adjust content
2. Copy perl binary `xferlogd` in `/usr/sbin/xferlogd`
3. Copy systemd unit file `xferlogd.service` in `/var/systemd/systeù/xferlogd.service` and reload systemd with command `systemctl reload-daemon`
4. Create a FIFO file by running command `mkfifo /var/log/proftpd/xferlog.fifo` (adjust file path to what you set in configuration file)
5. Start xferlogd by running command `systemctl enable xferlogd && systemctl start xferlogd`
6. Change Proftpd configuration file `/etc/proftpd/proftpd.conf` and update the following line:
```
TransferLog /var/log/proftpd/xferlog.fifo
```
7. Restart proftpd
