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