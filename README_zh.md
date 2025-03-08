
/home/homeassistant/.homeassistant
~~~
docker run -d \
  --name ha \
  --privileged \
  --restart=unless-stopped \
  -e TZ=America/Los_Angeles \
  -v /home/homeassistant/.homeassistant:/config \
  -v /run/dbus:/run/dbus:ro \
  --network=host \
  ghcr.io/home-assistant/home-assistant:stable
~~~

~~~

  services:
  homeassistant:
    container_name: homeassistant
    image: "ghcr.io/home-assistant/home-assistant:stable"
    volumes:
      - /opt/homeassistant/config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
    privileged: true
    network_mode: host
~~~


sudo docker compose up -d

~~~
将 STT 和 home assistant 服务打包并且用 compose 进行编排：

services:
  stt:
    build: ./stt
    ports:
      - "6006:6006"

  home_assistant:
    image: "ghcr.io/home-assistant/home-assistant"
    ports:
      - "8123:8123"
    environment:
      - TZ=Asia/Shanghai
      - OPENAI_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
    volumes:
      - ./ha_config:/config

~~~