# debian 12  + docker rpi p5b

# systemctl status NetworkManager
~~~
systemctl status NetworkManager
● NetworkManager.service - Network Manager
     Loaded: loaded (/lib/systemd/system/NetworkManager.service; enabled; preset: enabled)
     Active: active (running) since Sun 2025-05-18 03:24:49 CST; 3 days ago
       Docs: man:NetworkManager(8)
   Main PID: 666 (NetworkManager)
      Tasks: 3 (limit: 9585)
        CPU: 36.455s
     CGroup: /system.slice/NetworkManager.service
             └─666 /usr/sbin/NetworkManager --no-daemon

May 18 22:07:05 raspberrypi NetworkManager[666]: <info>  [1747577225.7905] device (br-caefea183540): carrier: link connected
May 19 02:21:33 raspberrypi NetworkManager[666]: <info>  [1747592493.5298] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000
May 19 07:05:37 raspberrypi NetworkManager[666]: <info>  [1747609537.5878] manager: (veth8613b62): new Veth device (/org/freedesktop/NetworkManager/Devices/13)
May 19 07:06:35 raspberrypi NetworkManager[666]: <info>  [1747609595.3993] manager: (vethf212d1a): new Veth device (/org/freedesktop/NetworkManager/Devices/14)
May 19 07:06:35 raspberrypi NetworkManager[666]: <info>  [1747609595.4227] device (vethf212d1a): carrier: link connected
May 19 07:06:35 raspberrypi NetworkManager[666]: <info>  [1747609595.4230] device (br-caefea183540): carrier: link connected
May 19 14:11:36 raspberrypi NetworkManager[666]: <info>  [1747635096.5924] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000
May 20 01:16:51 raspberrypi NetworkManager[666]: <info>  [1747675011.0430] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000
May 20 12:14:27 raspberrypi NetworkManager[666]: <info>  [1747714467.5322] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000
May 20 23:32:44 raspberrypi NetworkManager[666]: <info>  [1747755164.9582] dhcp6 (eth0): state changed new lease, address=fd00::d29f::1000

~~~