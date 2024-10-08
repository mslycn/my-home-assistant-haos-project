Configure Docker to use a proxy server

## Dockerd 代理

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


## Container 代理

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

https://www.cnblogs.com/pgyLang/p/17789930.html

https://docs.docker.com/network/proxy/
