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