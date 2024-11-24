# HASSOS

## Docker配置系列

~~~
Docker的网络配置 2 配置 DNS和主机名
Docker的网络配置 3 user-defined网络
Docker的网络配置 4 内嵌的DNS server
Docker的网络配置 5 将容器与外部世界连接
Docker的网络配置 6 docker-proxy
Docker的网络配置 7 docker pull断点续传设置

开启容器的 IPv6 功能
~~~

开启容器的 IPv6 功能
~~~
cat > /etc/docker/daemon.json << EOF
{
    "log-driver": "json-file",
    "log-opts": {
        "max-size": "20m",
        "max-file": "3"
    },
    "ipv6": true,
    "fixed-cidr-v6": "fd00:dead:beef:c0::/80",
    "experimental":true,
    "ip6tables":true
}
EOF

~~~


## Docker更新容器镜像的三种方法
~~~
更新用Docker命令部署的应用

更新用Docker-compose部署的应用

安装并利用Portainer更新

~~~

~~~
docker cli
docker-compose

~~~

~~~
docker容器随宿主机开机自启动 Start containers automatically

cat > /etc/docker/daemon.json <<EOF
{
    "log-driver": "json-file",
    "log-opts": {
        "max-size": "20m",
        "max-file": "3"
    },
    "ipv6": true,
    "fixed-cidr-v6": "fd00:dead:beef:c0::/80",
    "experimental":true,
    "ip6tables":true,
    "registry-mirrors": [
      "https://docker.m.daocloud.io",
      "https://dockerhub.icu",
      "https://docker.anyhub.us.kg",
      "https://docker.1panel.live"
    ]
}
EOF

~~~


~~~
Docker磁盘空间使用分析与清理


~~~


## 开发文档

[《HASSOS 使用指南》](https://sscms.com/docs/v7/getting-started/)

[《HASSOS 系统更新》](https://sscms.com/docs/v7/updates/)

[《HASSOS STL 语言》](https://sscms.com/docs/v7/stl/)

[《HASSOS 插件开发》](https://sscms.com/docs/v7/plugin/)

[《SSCMS 官方插件》](https://sscms.com/docs/v7/official/)

[《HASSOS 命令行》](https://sscms.com/docs/v7/cli/)

[《HASSOS REST API》](https://sscms.com/docs/v7/api/)

[《HASSOS 数据结构》](https://sscms.com/docs/v7/model/)

## HASSOS 源码结构

```code
│ sscms.sln                  Visual Studio 项目文件
│
├─docker                      Docker 配置文件
├─src/Datory                  数据库基础类
├─src/SSCMS                   接口、基础类
├─src/SSCMS.Cli               命令行工具
├─src/SSCMS.Core              CMS核心代码
├─src/SSCMS.Web               CMS App
└─tests                       测试
```

## 发布跨平台版本

### Window(x64)：

```
npm install
npm run build-win-x64
dotnet build ./build-win-x64/build.sln -c Release
dotnet publish ./build-win-x64/src/SSCMS.Cli/SSCMS.Cli.csproj -r win-x64 -c Release -o ./publish/sscms-win-x64
dotnet publish ./build-win-x64/src/SSCMS.Web/SSCMS.Web.csproj -r win-x64 -c Release -o ./publish/sscms-win-x64
npm run copy-win-x64
```

> Note: 进入文件夹 `./publish/sscms-win-x64` 获取最终发布版本

### Window(x32)：

```
npm install
npm run build-win-x32
dotnet build ./build-win-x32/build.sln -c Release
dotnet publish ./build-win-x32/src/SSCMS.Cli/SSCMS.Cli.csproj -r win-x32 -c Release -o ./publish/sscms-win-x32
dotnet publish ./build-win-x32/src/SSCMS.Web/SSCMS.Web.csproj -r win-x32 -c Release -o ./publish/sscms-win-x32
npm run copy-win-x32
```

> Note: 进入文件夹 `./publish/sscms-win-x32` 获取最终发布版本

### Linux(x64)：

```
npm install
npm run build-linux-x64
dotnet build ./build-linux-x64/build.sln -c Release
dotnet publish ./build-linux-x64/src/SSCMS.Cli/SSCMS.Cli.csproj -r linux-x64 -c Release -o ./publish/sscms-linux-x64
dotnet publish ./build-linux-x64/src/SSCMS.Web/SSCMS.Web.csproj -r linux-x64 -c Release -o ./publish/sscms-linux-x64
npm run copy-linux-x64
```

> Note: 进入文件夹 `./publish/sscms-linux-x64` 获取最终发布版本

### Linux(arm64)：

```
npm install
npm run build-linux-arm64
dotnet build ./build-linux-arm64/build.sln -c Release
dotnet publish ./build-linux-arm64/src/SSCMS.Cli/SSCMS.Cli.csproj -r linux-arm64 -c Release -o ./publish/sscms-linux-arm64
dotnet publish ./build-linux-arm64/src/SSCMS.Web/SSCMS.Web.csproj -r linux-arm64 -c Release -o ./publish/sscms-linux-arm64
npm run copy-linux-arm64
```

> Note: 进入文件夹 `./publish/sscms-linux-arm64` 获取最终发布版本

## 在 Docker 中运行

拉取最新版本的 SSCMS 镜像

```sh
docker pull sscms/core:latest
```

运行 SSCMS 容器

```sh
docker run -d \
    --name my-sscms \
    -p 80:80 \
    --restart=always \
    -v volume-sscms:/app/wwwroot \
    -e SSCMS_SECURITY_KEY=e2a3d303-ac9b-41ff-9154-930710af0845 \
    -e SSCMS_DATABASE_TYPE=SQLite \
    sscms/core
```

## 贡献代码

项目编译需要使用 Visual Studio 2022，你可以从这里下载 [Visual Studio Community 2022](https://www.visualstudio.com/downloads/)

代码贡献有很多形式，从提交问题，撰写文档，到提交代码，我们欢迎任何形式的贡献！

## 系统更新

SSCMS 产品将每隔两月发布新的正式版本，我们将在每次迭代中对核心功能、文档支持、功能插件以及网站模板四个方面进行持续改进。

## 问题与建议

如果发现任何 BUG 以及对产品使用的问题与建议，请提交至 [Github Issues](https://github.com/siteserver/cms/issues) 或者 [Gitee Issues](https://gitee.com/siteserver/cms/issues)。

## 关注最新动态

[![qrcode](https://sscms.com/assets/images/qrcode_for_wx.jpg)](https://sscms.com/)

## 特别声明

SSCMS 项目已加入 [dotNET China](https://gitee.com/dotnetchina)  组织。<br/>

![dotnetchina](https://gitee.com/dotnetchina/home/raw/master/assets/dotnetchina-raw.png "dotNET China LOGO")

## License

[GNU Affero General Public License v3.0](LICENSE)

Copyright (C) 2003-2023 SSCMS

