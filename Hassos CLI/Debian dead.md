HA very slow. is it the hardware

## problem
these problems should also occur with a fresh install. I didn’t install many addons yet. I went to the Homeassistant Supervisor and turned on the memory and CPU usage. they are all very low, but HA is very unresponsive. when I click for example to load HACS. the whole system is unavailable for at least 10 minutes

## HACS

- Was HACS installed recently? I do not know if it is still the case, but when freshly installed HACS used to warn about accessing many github repositories (first install only). Tht would take a very long time and slow things down until done. HACS was overhauled to require less from github, so that might have changed.

- VS Studio Code Addon
If it is the VS Studio Code Addon, then it can happen on a fresh install too.
It is the Lint that is causing it, so just opening up the addon can make it go haywire.

## ha side
If it’s a problem with an integration or a memory leak changing hardware won’t save you.

ha side
See “sensor.memory_use” history if it’s rising gradually. If it’s not available enable it in system monitor.

See “sensor.memory_use” history if it’s rising gradually. If it’s not available enable it in system monitor.
There can be memory hog addons, Studio Code Server is one of them. I restart studio addon every night at 00:00 to prevent this.

Often this is an addon or integration misbehaving. Either hogging cpu, or more often, repeatedly requesting large amounts of memory and not return it to the system when done. For me, Studio Code Server is often the culprit.

You might want to head to the Homeassistant Supervisor in the integrations tab, turn on all the addons sensors for memory and cpu and put those in a graph to see if something stands out. Also put total memory and cpu for HA in those graphs. If it is an integration, it will be HA itself standing out.


