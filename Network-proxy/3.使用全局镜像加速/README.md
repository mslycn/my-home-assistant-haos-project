
README-use a registry-mirrors

## Docker镜像加速原理
Docker镜像加速主要是通过使用国内的Docker Registry服务器来实现的。这些服务器可以更快地响应请求，从而提高镜像拉取的速度。常见的国内镜像加速器包括阿里云、腾讯云、网易等。


若我们使用一台魔法机器从 gcr.io 或 quay.io 等仓库先把我们无法下载的镜像拉取下来，然后重新上传到 docker.io ，是不是就可以使用 Docker Hub 的镜像加速器来下载了

镜像加速

原文链接：https://neucrack.com/p/286




分2种情况使用加速器

- docker 使用加速器

- containerd 使用加速器

https://www.cnblogs.com/jingjingxyk/p/16574995.html


## 配置镜像加速器

在 Docker 中，可以修改daemon.json来修改镜像仓库.

Docker镜像加速主要是通过使用国内的Docker Registry服务器来实现的.

针对Docker客户端版本大于 1.10.0 的用户

可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器.

sudo vim /etc/docker/daemon.json

~~~
{
  "registry-mirrors": ["https://ghcr.nju.edu.cn"]
}
~~~

### aliyun镜像源

1. 获取aliyun镜像源

menu path：容器镜像服务/镜像加速器
https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors

First, edit your /etc/docker/daemon.json file (create it if it doesn't exist using sudo) and add the following content:
~~~
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://iao.mirror.aliyuncs.com"]
}
EOF
~~~

2. Next, restart your Docker daemon by running:

通过修改 dockerd 配置文件，并重载，可以在服务器上开启 dockerd 的属性

~~~
sudo systemctl daemon-reload
sudo systemctl restart docker
~~~


### nju镜像源

使用的容器需要从github下载镜像，服务器在国外下载速度很慢，提供镜像加速的方案

sudo vim /etc/docker/daemon.json

~~~
{
  "registry-mirrors": ["https://ghcr.nju.edu.cn"]
}
~~~

useful links

https://zhuanlan.zhihu.com/p/668299752