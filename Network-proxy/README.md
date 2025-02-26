


## Docker hub && docker github  && Huggingface space

ghcr.io直接下载速度很慢



Docker安装由于网络问题很少能自己拉取成功，常用的方法有几种：

- 更换Docker镜像源

- 使用喂屁嗯

- 手动下载镜像

Docker安装由于网络问题很少能自己拉取成功，常用的方法有几种

- 离线导出和导入

  找到可以正常运行的服务器，使用docker save备份镜像，复制到目标机器后用docker load导入。

- 搭建Docker私有仓库

  把镜像存储在自己的服务器上。

- 在使用时替换docker位置，要么修改/etc/docker/daemon.json。

                        


Docker镜像和容器的导出、导入操作及其区别

Docker私有仓库搭建（Registry）

将镜像上传至dockerhub官网






Docker私有仓库搭建（Registry）

https://www.cnblogs.com/wangcuican/p/12152725.html


- 使用时替换docker位置

原来地址：redis:7.0.14-alpine  # 这个是官方镜像，省略了前边的域名
替换地址：docker.your_domain_name/redis:7.0.14-alpine

- 使用时修改/etc/docker/daemon.json

~~~
{
  "registry-mirrors": [
    "https://docker.your_domain_name"
  ]
}
~~~


## 查看日志
查看Docker日志以获取更多错误信息：

journalctl -u docker.service


查看 Docker 镜像信息，使用以下命令：

docker info  

在 HassOS 中，Docker 的配置文件位于 /etc/docker/daemon.json。

sudo nano /etc/docker/daemon.json  

修改/etc/docker/daemon.json文件来加速访问。

## Note

hassos 不允许直接编辑 docker 的配置文件，所以你不能用通常的方法修改 /etc/docker/daemon.json 添加国内可用镜像源。在Home Assistant OS下，该文件是只读的，无法直接进行修改.

但 hassos 可以直接通过 udev 规则将 docker 配置文件 daemon.json 更改为所需的配置。
最重要的是，当 hassos 更新到新版本时，所配置 udev 规则不会被覆盖。

## 在Home Assistant OS下，该文件是只读的，无法直接进行修改。


## Way 1.通过USB driver 修改

3. 编辑配置文件daemon
在打开的配置文件中，您将看到以下内容：
~~~
{  
  "debug": true,  
  "exec-opts": ["native.cgroupdriver=systemd"],  
  "group": "docker",  
  "hosts": ["unix:///var/run/docker.sock", "tcp://0.0.0.0:2375"],  
  "log-driver": "json-file",  
  "log-opts": {  
    "max-size": "10m",  
    "max-file": "3"  
  },  
  "storage-driver": "overlay2",  
  "storage-opts": [  
    "overlay2.override_kernel_check=true"  
  ]  
}  
~~~

添加镜像源

在配置文件中，找到 "registry-mirrors" 键，并添加您选择的镜像源。以下是一些常用的国内镜像源：

{  
  "registry-mirrors": [  
    "https://docker.mirrors.ustc.edu.cn",  
    "https://hub-mirror.c.163.com",  
    "https://<your-id>.mirror.aliyuncs.com"  
  ]  
}  
3.4 保存并退出

编辑完成后，保存并退出配置文件。

sudo systemctl daemon-reload  
sudo systemctl restart docker  


Way2. 配置 udev 规则

Note

hassos 不允许直接编辑 docker 的配置文件，所以你不能用通常的方法修改 /etc/docker/daemon.json 添加国内可用镜像源。但 hassos 可以直接通过 udev 规则将 docker 配置文件 daemon.json 更改为所需的配置。
最重要的是，当 hassos 更新到新版本时，所配置 udev 规则不会被覆盖。

https://bbs.hassbian.com/thread-26549-1-1.html

在/etc/udev/rules.d中建立两个文件

https://mansmarthome.info/posts/home-assistant/obkhod-blokirovki-docker-hub/

在/etc/udev/rules.d中建立两个文件，一个是规则文件00-docker-mirrors-workaround.rules，用于在开机的时候通过配置的规则覆盖默认的daemon.json。另一个是自定义的docker-daemon.json，用来覆盖默认的文件。

00-docker-mirrors-workaround.rules的内容是：

~~~
ENV{ID_FS_LABEL}="hassos-overlay", ACTION=="change", RUN+="/usr/bin/systemd-mount --no-block -o bind /etc/udev/rules.d/docker-daemon.json /etc/docker/daemon.json"

~~~

https://hafuhafu.com/archives/install-home-assistant-os-on-esxi/


## other

