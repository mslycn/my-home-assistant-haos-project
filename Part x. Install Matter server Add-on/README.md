Matter-server with docker not working correctly

Matter require an enabled and working IPv6 network.
DNSSD is DNS discovery for IPv6.

- Add-ons:
Matter Server Add-on
OpenThread Border Router Add-on


## Install Home Assistant Add-on: OpenThread Border Router Add-on（通用）

This requires a supported 802.15.4 capable radio with OpenThread RCP firmware. like as: Home Assistant Connect ZBT-1

用这个add on，需要刷OpenThread RCP firmware




## Home Assistant Add-on: SiliconLabs Zigbee/OpenThread Multiprotocol Add-on（SiliconLabs专用）

This add-on allows you to use Zigbee and OpenThread protocol simultaneous on a single Silicon Labs based radio. The radio needs the RCP Multi-PAN firmware installed to support multiple IEEE 802.15.4 Personal Area Networks (PAN). The addon has been tested with EFR32 Series 2 based radios.

Zigbee/OpenThread Multiprotocol container for Silicon Labs based radios such as Home Assistant Yellow, Home Assistant SkyConnect, and Home Assistant Connect ZBT-1.

用这个add on，需要刷多协议固件

