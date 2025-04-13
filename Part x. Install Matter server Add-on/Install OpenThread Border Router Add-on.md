
##  how to use Connect ZBT-1 to turn your Home Assistant into a Thread Border router

Home Assistant Connect ZBT-1

step 1.The OpenThread Border Router add-on flashes the Thread firmware on startup.
Install Home Assistant Add-on: OpenThread Border Router Add-on

This requires a supported 802.15.4 capable radio with OpenThread RCP firmware. Home Assistant Connect ZBT-1


## Integration:

- Thread
- Open Thread Boarder Router
- Matter
- Homekit device (Have a Homekit Thread device) 
## Add-ons:
- Matter Server
- OpenThread Border Router


This add-on allows you to form  a Thread network and make Home Assistant a Thread Border Router.

This add-on allows you to join a Thread network and make Home Assistant a Thread Border Router.


docker pull homeassistant/amd64-addon-otbr:2.13.0

~~~~
安装加载项失败
Can't install homeassistant/amd64-addon-otbr:2.13.0: 500 Server Error for http+docker://localhost/v1.47/images/create?tag=2.13.0&fromImage=homeassistant%2Famd64-addon-otbr&platform=linux%2Famd64: Internal Server Error ("Get "https://registry-1.docker.io/v2/": net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)")
~~~~






https://github.com/home-assistant/addons/tree/master/openthread_border_router