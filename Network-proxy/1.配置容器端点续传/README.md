1. Docker Registry 提供了 RESTful API，允许直接与镜像仓库交互。可以使用这些 API 来分块下载镜像的层（layers），并实现断点续传。

2. 分块下载镜像层
一个Docker镜像由多个镜像层组成，每个层可以通过 API 单独下载。可以使用多线程来并行下载这些层，以提高下载速度。

3. 在下载过程中，记录已下载的字节数。如果下载中断，可以从上次中断的位置继续下载。

### Docker开启断点续传属性
通过修改 dockerd 配置文件，并重载，可以在服务器上开启 dockerd 的断点续传属性。修改配置文件 /etc/docker/daemon.json

添加 "features": {"containerd-snapshotter": true}

修改后的配置文件如下：

vi /etc/docker/daemon.json

single line
~~~
{
     "features": {"containerd-snapshotter": true}
}

~~~

multi line
~~~
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "features": {"containerd-snapshotter": true},
  "experimental": true,
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://hub.rat.dev",
    "https://docker.1panel.live"
  ]
}

~~~

- 重启 Docker 守护进程，使配置生效
~~~
systemctl daemon-reload
$ sudo systemctl restart docker
~~~

注意：

1. 开启该配置以后，会导致原来下载的镜像文件被隐藏，开启和关闭该配置的情况下，镜像文件是隔离存储的（OrbStack下验证）

2. docker ps -a 运行的容器也不见了

3. 重新关闭该配置，以前的镜像和运行的容器，会重新出现



- 查看docker 是否开启experimental功能
docker system info

Debug Mode: false
 Experimental: true
