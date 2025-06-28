Home Assistant Community Add-on: Advanced SSH & Web Terminal

With the Official SSH addon, everything works as expected.

Thats my config.

~~~

{
  "log_level": "info",
  "port": 22,
  "username": "myuser",
  "password": "xxxxx",
  "authorized_keys": [],
  "sftp": false,
  "compatibility_mode": true,
  "allow_agent_forwarding": false,
  "allow_remote_port_forwarding": true,
  "allow_tcp_forwarding": false,
  "packages": [],
  "init_commands": []
}
~~~~