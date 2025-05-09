## Note
目前最新haos 13.1已经不能修改docker的配置，即不能添加代理。长远方法是使用透明代理


Configure Docker to use a proxy server

使用代理解决Docker拉取镜像失败问题

在Linux环境下，可以通过编辑Docker配置文件来设置代理。

代理服务器的问题也可能存在。如果用户处于需要代理的网络环境中，而Home Assistant没有正确配置代理，那么无法连接到外部服务器。这时候需要检查Home Assistant的代理设置，或者在Docker环境中配置代理变量。

1. 首先， docker pull / docker push 和 docker build/docker run 使用代理的方式不一样


原文链接：https://neucrack.com/p/286




2. 给Docker服务配置代理

镜像的拉取pull和管理都是 docker daemon 的职责，所以我们要让 docker daemon 知道代理服务器的存在。而 docker daemon 是由 systemd 管理的，所以我们要从 systemd 配置入手。

source:https://www.cnblogs.com/abc1069/p/17496240.html

3. Dockerd代理 - docker pull的正确代理设置

docker pull /push 的代理被 systemd 接管，所以需要设置 systemd

- 找到 Docker service 的文件，直接在 [Service] 模块下加入代理配置
~~~
# 通过 systemctl status 可以看到 Service 文件目录 
$ sudo systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: enabled)

$ sduo vi /usr/lib/systemd/system/docker.service
~~~


~~~
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo touch /etc/systemd/system/docker.service.d/proxy.conf
~~~


docker daemon 使用 HTTP_PROXY, HTTPS_PROXY, 和 NO_PROXY 三个环境变量配置代理服务器，但是你需要在 systemd 的文件里配置环境变量，而不能配置在 daemon.json 里。

在执行docker pull时，是由守护进程dockerd来执行。因此，代理需要配在dockerd的环境中。而这个环境，则是受systemd所管控，因此实际是systemd的配置


## 设置Docker使用代理

1. 编辑Docker配置文件
sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf

2. 添加以下内容：
~~~
[Service]
Environment="HTTP_PROXY=http://proxy.example.com:8080/"
Environment="HTTPS_PROXY=http://proxy.example.com:8080/"
Environment="NO_PROXY=localhost,127.0.0.1,.example.com"
~~~
这里的127.0.0.1是直接用了本机的 http 代理，然后重启服务才能生效

3. 重载Systemd管理器配置并重启Docker服务
~~~
sudo systemctl daemon-reload
sudo systemctl restart docker
~~~

可以通过sudo systemctl show --property=Environment docker看到设置的环境变量。

然后docker pull就会使用代理.

这里 HTTP 代理可以通过你的代理软件开出来，如果你的代理软件只能开出来 socks5 代理的话，你可以用 polipo 开一个 http 代理使用


3. Container代理 - docker run 时的代理设置 - 设置 docker 全局代理

这种设置方法只对 build 和 run 有用


在容器运行阶段，如果需要代理上网，则需要配置 ~/.docker/config.json。以下配置，只在Docker 17.07及以上版本生效。

Configure the Docker client
You can add proxy configurations for the Docker client using a JSON configuration file, located in ~/.docker/config.json. Builds and containers use the configuration specified in this file.

vim ~/.docker/config.json

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

注意:

仅支持 http https ftp 协议，不支持 socks5 协议（2022.3.24，未来不一定，官方文档为准），可以使用polipo创建一个http代理服务，参考https://neucrack.com/p/275

这里使用了172.17.0.1(docker 虚拟网卡地址), 而不是127.0.0.1, 这是因为这是从容器内部的角度来看的, 容器内部要使用代理,默认情况下只能访问这个虚拟网卡的地址, 127.0.0.1是容器内部, 如果代理在宿主机, 要使用 虚拟网卡的地址才能访问到.

这个文件一旦存在, docker就会使用这里面的代理, 包括创建的容器都会使用它。 所以不需要代理了, 需要关闭代理, 就是把文件重命名一下就好了, 这点用起来确实挺麻烦，也许未来会优化体验吧。

注意， 一个容器一旦生成， 这些环境变量（http_proxy https_proxy ftp_proxy no_proxy）就会被继承到容器中， 就算把config.json删除， 这个容器依然使用创建时的环境变量，可以手动在容器内重新设置这些环境变量， 这点也挺容易让人头疼的， 一定要注意。

https://docs.docker.com/network/proxy/




## Docker Build 代理

虽然 docker build 的本质，也是启动一个容器，但是环境会略有不同，用户级配置无效。在构建时，需要注入 http_proxy 等参数。

detail:
https://www.cnblogs.com/abc1069/p/17496240.html

https://www.cnblogs.com/pgyLang/p/17789930.html

https://docs.docker.com/network/proxy/



原文链接：https://blog.csdn.net/weixin_74313592/article/details/145215879

https://gitee.com/wanfeng789/docker-hub#%E4%BD%BF%E7%94%A8%E4%BB%A3%E7%90%86%E6%8B%89%E5%8F%96%E9%95%9C%E5%83%8F