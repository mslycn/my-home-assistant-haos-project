
/home/homeassistant/.homeassistant

docker run -d \
  --name ha \
  --privileged \
  --restart=unless-stopped \
  -e TZ=America/Los_Angeles \
  -v /home/homeassistant/.homeassistant:/config \
  -v /run/dbus:/run/dbus:ro \
  --network=host \
  ghcr.io/home-assistant/home-assistant:stable