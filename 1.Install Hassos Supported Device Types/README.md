
## Latest Data information of HassOS

List of Hardware devices are supported by HassOS
https://github.com/home-assistant/operating-system/blob/dev/Documentation/boards/README.md

Latest kernel of HassOS
https://github.com/home-assistant/operating-system/blob/dev/Documentation/kernel.md

Latest Home Assistant OS versions data
https://github.com/home-assistant/version/blob/master/stable.json

## Check HassOS Version & Platform Support




Manual Network Configuration in HassOS
https://github.com/home-assistant/operating-system/blob/dev/Documentation/network.md


## HassOS Debug

use an USB drive  to configure network options, install updates 
https://github.com/home-assistant/operating-system/blob/dev/Documentation/configuration.md

Raspberry Pi /dev
https://bbs.hassbian.com/thread-26549-1-1.html


## Supported Device Types

Latest Home Assistant OS versions data

https://github.com/home-assistant/version/blob/master/stable.json

~~~
{
  "channel": "stable",
  "supervisor": "2024.12.3",
  "homeassistant": {
    "default": "2025.1.0",
    "qemux86": "2025.1.0",
    "qemux86-64": "2025.1.0",
    "qemuarm": "2025.1.0",
    "qemuarm-64": "2025.1.0",
    "generic-x86-64": "2025.1.0",
    "intel-nuc": "2025.1.0",
    "khadas-vim3": "2025.1.0",
    "raspberrypi": "2025.1.0",
    "raspberrypi2": "2025.1.0",
    "raspberrypi3": "2025.1.0",
    "raspberrypi3-64": "2025.1.0",
    "raspberrypi4": "2025.1.0",
    "raspberrypi4-64": "2025.1.0",
    "raspberrypi5-64": "2025.1.0",
    "yellow": "2025.1.0",
    "green": "2025.1.0",
    "tinker": "2025.1.0",
    "odroid-c2": "2025.1.0",
    "odroid-c4": "2025.1.0",
    "odroid-m1": "2025.1.0",
    "odroid-n2": "2025.1.0",
    "odroid-xu": "2025.1.0"
  },
  "hassos": {
    "ova": "14.1",
    "rpi2": "14.1",
    "rpi3": "14.1",
    "rpi3-64": "14.1",
    "rpi4": "14.1",
    "rpi4-64": "14.1",
    "rpi5-64": "14.1",
    "yellow": "14.1",
    "green": "14.1",
    "tinker": "14.1",
    "odroid-c2": "14.1",
    "odroid-c4": "14.1",
    "odroid-m1": "14.1",
    "odroid-m1s": "14.1",
    "odroid-n2": "14.1",
    "odroid-xu4": "14.1",
    "generic-x86-64": "14.1",
    "generic-aarch64": "14.1",
    "khadas-vim3": "14.1"
  },

~~~

hassos ota

~~~
"ota": "https://os-artifacts.home-assistant.io/{version}/{os_name}_{board}-{version}.raucb",
~~~

Home Assistant offers four different installation methods.

We recommend using the following  method:

Home Assistant Operating System


Home Assistant OS虚拟机版



最新 Home Assistant OS 针对树莓派平台已经预装了 Matter 和 Thread.


