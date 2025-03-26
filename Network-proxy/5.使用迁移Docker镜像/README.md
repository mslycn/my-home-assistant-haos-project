docker save && docker load 

## 离线导出和导入

找到可以正常运行的服务器，使用docker save备份镜像，复制到目标机器后用docker load导入即可.

申请国外站点，比如腾讯云的新加坡站点，几十块一年，每月有1024G流量，自己使用足够.

打包镜像到本地
1. 压缩保存镜像到本地

docker save 镜像名 > 镜像名.tar
docker pull homeassistant/<image-name>
docker save -o <image-name>.tar homeassistant/<image-name>

2：手动上传到另一个服务器

3. 另一个服务器解压镜像

docker load < 镜像名.tar

docker load -i <image-name>.tar

4：查看镜像

docker images

##  https://registry-1.docker.io

Can't install homeassistant/amd64-addon-speech-to-phrase:1.3.0: 500 Server Error for http+docker://localhost/v1.47/images/create?tag=1.3.0&fromImage=homeassistant%2Famd64-addon-speech-to-phrase&platform=linux%2Famd64: Internal Server Error ("Get "https://registry-1.docker.io/v2/": net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)")

docker pull homeassistant/amd64-addon-speech-to-phrase:1.3.0

docker load -i <image-name>.tar


hugggingface.co无法访问
Useful links

https://www.iaspnetcore.com/Blog/BlogPost/66f3363e3e98ac0270269578/docker-copy-instruction