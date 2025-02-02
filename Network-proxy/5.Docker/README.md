Configure Docker to use a proxy server

镜像的拉取和管理都是 docker daemon 的职责，所以我们要让 docker daemon 知道代理服务器的存在。而 docker daemon 是由 systemd 管理的，所以我们要从 systemd 配置入手。

source:https://www.cnblogs.com/abc1069/p/17496240.html

## Dockerd代理 - docker pull的正确代理设置

docker daemon 使用 HTTP_PROXY, HTTPS_PROXY, 和 NO_PROXY 三个环境变量配置代理服务器，但是你需要在 systemd 的文件里配置环境变量，而不能配置在 daemon.json 里。

在执行docker pull时，是由守护进程dockerd来执行。因此，代理需要配在dockerd的环境中。而这个环境，则是受systemd所管控，因此实际是systemd的配置

~~~
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo touch /etc/systemd/system/docker.service.d/proxy.conf


~~~

~~~
[Service]
Environment="HTTP_PROXY=http://proxy.example.com:8080/"
Environment="HTTPS_PROXY=http://proxy.example.com:8080/"
Environment="NO_PROXY=localhost,127.0.0.1,.example.com"
~~~

## Container 代理 - docker run 时的代理设置

在容器运行阶段，如果需要代理上网，则需要配置 ~/.docker/config.json。以下配置，只在Docker 17.07及以上版本生效。

Configure the Docker client
You can add proxy configurations for the Docker client using a JSON configuration file, located in ~/.docker/config.json. Builds and containers use the configuration specified in this file.
~~~
{
 "proxies": {
   "default": {
     "httpProxy": "http://proxy.example.com:3128",
     "httpsProxy": "https://proxy.example.com:3129",
     "noProxy": "*.test.example.com,.example.org,127.0.0.0/8"
   }
 }
}
~~~

## Docker Build 代理

虽然 docker build 的本质，也是启动一个容器，但是环境会略有不同，用户级配置无效。在构建时，需要注入 http_proxy 等参数。

detail:
https://www.cnblogs.com/abc1069/p/17496240.html

https://www.cnblogs.com/pgyLang/p/17789930.html

https://docs.docker.com/network/proxy/

