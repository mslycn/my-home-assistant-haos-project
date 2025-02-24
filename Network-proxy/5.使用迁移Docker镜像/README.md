docker save && docker load 


打包镜像到本地
1：压缩保存镜像到本地

docker save 镜像名 > 镜像名.tar
2：手动上传到另一个服务器

3：另一个服务器解压镜像

docker load < 镜像名.tar
4：查看镜像

docker images