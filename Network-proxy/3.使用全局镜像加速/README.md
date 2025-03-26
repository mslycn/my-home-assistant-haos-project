
README-use a registry-mirrors

## Docker镜像加速原理
Docker镜像加速主要是通过使用国内的Docker Registry服务器来实现的。这些服务器可以提高镜像拉取的速度。常见的国内镜像加速器包括阿里云、腾讯云、网易等。


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
  "registry-mirrors": [
    "https://docker.m.daocloud.io",
    "https://registry.docker-cn.com",
    "https://mirror.ccs.tencentyun.com"
  ]
}
~~~

2. Next, restart your Docker daemon by running:

通过修改 dockerd 配置文件，并重载，可以在服务器上开启 dockerd 的属性

~~~
sudo systemctl daemon-reload
sudo systemctl restart docker
~~~




useful links

https://zhuanlan.zhihu.com/p/668299752