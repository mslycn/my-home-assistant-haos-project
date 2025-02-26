1. Docker Registry 提供了 RESTful API，允许直接与镜像仓库交互。可以使用这些 API 来分块下载镜像的层（layers），并实现断点续传。

2. 分块下载镜像层
Docker 镜像由多个层组成，每个层可以通过 API 单独下载。可以使用多线程来并行下载这些层，以提高下载速度。

3. 在下载过程中，记录已下载的字节数。如果下载中断，可以从上次中断的位置继续下载。

### 开启属性
通过修改 dockerd 配置文件，并重载，可以在服务器上开启 dockerd 的实验属性。为配置文件 /etc/docker/daemon.json

添加 “experimental”: true。

修改后的配置文件看起来和下面的比较像：
~~~
{
  "experimental": true
}

~~~


~~~
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "experimental": true,
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://hub.rat.dev",
    "https://docker.1panel.live"
  ]
}

~~~