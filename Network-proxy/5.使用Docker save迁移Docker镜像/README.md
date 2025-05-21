
## 应用
现在临时在其他机器docker pull，docker save；然后拷贝到haos里，执行docke load 导入image。然后在ha的web里进行matter 的配置（docker就会启动这个image）

docker search --filter architecture=arm64 eclipse-mosquitto

### Step 1. 使用 docker pull 拉取特定架构amd64、arm64、aarch64的容器镜像
强制指定目标平台，要求 Docker 拉取 ARM64 版本的镜像。

注意：此方法仅在官方镜像实际支持多架构时有效，否则仍需使用专用仓库。
~~~
docker pull --platform linux/arm64  homebridge/homebridge

docker pull --platform linux/arm64 linuxserver/kodi-headless (failure)

docker pull --platform linux/arm64 linuxserver/code-server  

docker pull openthread/otbr:latest
docker pull --platform linux/arm64 openthread/otbr:latest
docker pull --platform linux/arm64 eclipse-mosquitto
docker pull --platform linux/arm64 rhasspy/wyoming-vosk
~~~

http://localhost:4999/boards/topic/40217



### Step 2. docker save && docker load 

## 离线导出和导入

找到可以正常运行的服务器，使用docker save备份镜像，复制到目标机器后用docker load导入即可.

申请国外站点，比如腾讯云的新加坡站点，几十块一年，每月有1024G流量，自己使用足够.

打包镜像到本地

### Step 2. 压缩保存镜像到本地

docker save 镜像名 > 镜像名.tar
docker pull homeassistant/<image-name>

### Step 3. 使用镜像的名字进行打包
docker save -o <image-name>.tar homeassistant/<image-name>

docker save -o  amd64-addon-speech-to-phrase.tar homeassistant/amd64-addon-speech-to-phrase:1.3.0  

docker save -o  amd64-addon-otbr.tar  homeassistant/amd64-addon-otbr:2.13.0

docker save -o otbr.tar openthread/otbr:latest

docker save -o wyoming-vosk.tar  rhasspy/wyoming-vosk  arm64

docker save -o eclipse-mosquitto.tar  eclipse-mosquitto arm64

docker save -o python-matter-server.tar  ghcr.io/home-assistant-libs/python-matter-server arm64

docker save -o linuxserver-code-server.tar linuxserver/code-server  arm64

linuxserver/kodi-headless


### Step 4.手动上传到另一个服务器

### Step 5. 另一个服务器解压镜像

docker load < 镜像名.tar >

docker load -i <image-name>.tar

docker load -i otbr.tar

docker load -i wyoming-piper.tar

docker load -i wyoming-vosk.tar  arm64

docker load -i eclipse-mosquitto.tar  arm64

docker load -i  python-matter-server.tar  

docker load -i linuxserver-code-server.tar 

### Step 6.查看镜像

docker images

##  https://registry-1.docker.io

Can't install homeassistant/amd64-addon-speech-to-phrase:1.3.0: 500 Server Error for http+docker://localhost/v1.47/images/create?tag=1.3.0&fromImage=homeassistant%2Famd64-addon-speech-to-phrase&platform=linux%2Famd64: Internal Server Error ("Get "https://registry-1.docker.io/v2/": net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)")

docker pull homeassistant/amd64-addon-speech-to-phrase:1.3.0

docker load -i <image-name>.tar


## 用命令查看多平台镜像的manifest信息

~~~
docker manifest inspect rhasspy/wyoming-vosk 
docker manifest inspect  ghcr.io/mslycn/wyoming-vosk-standalone
~~~
output
~~~
{
   "schemaVersion": 2,
   "mediaType": "application/vnd.oci.image.index.v1+json",
   "manifests": [
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 1050,
         "digest": "sha256:21404da367bb5bdcd5860b0e67f3c623a9fe617695582dcb4fba2f96a1adf83b",
         "platform": {
            "architecture": "amd64",
            "os": "linux"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 1050,
         "digest": "sha256:3d7500a0d739c7064485e0e813de15f43d5bbdaa415b1a9130ae1ca7c7ac019e",
         "platform": {
            "architecture": "arm64",
            "os": "linux"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 1050,
         "digest": "sha256:fc07bbc7c7aed0f0ee85d7de47ca0058a3a1172de44d8ea10e924eb8f8bd2256",
         "platform": {
            "architecture": "arm",
            "os": "linux",
            "variant": "v7"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 566,
         "digest": "sha256:8847cc24325b2b6f6a2da61c8a14054b586d7b06f2dd71c863626c30562fd098",
         "platform": {
            "architecture": "unknown",
            "os": "unknown"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 566,
         "digest": "sha256:b3c327a3f845dea908baaa5973418c4a0c320b7caba0da96057dc70def75349d",
         "platform": {
            "architecture": "unknown",
            "os": "unknown"
         }
      },
      {
         "mediaType": "application/vnd.oci.image.manifest.v1+json",
         "size": 566,
         "digest": "sha256:b4a7b34bfcdb7db9894a138372c0cfd5ecf49c1dde93a20c5e0d501c6b365114",
         "platform": {
            "architecture": "unknown",
            "os": "unknown"
         }
      }
   ]
}



~~~



rhasspy/wyoming-vosk 


hugggingface.co无法访问

Useful links

https://www.iaspnetcore.com/Blog/BlogPost/66f3363e3e98ac0270269578/docker-copy-instruction

https://www.cnblogs.com/cgy-home/p/15876862.html

## Getting Help

For further help, or general discussion, please use the Node-RED Forum


使用 docker pull 拉取特定架构amd64、arm64、aarch64的容器镜像
http://localhost:4999/boards/topic/40217/