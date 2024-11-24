# Custom Integration - HACS 

## Official web
~~~
https://github.com/hacs/integration/releases
~~~

~~~
https://github.com/hacs/integration/releases/download/1.34.0/hacs.zip
~~~


## 在线安装 - SSH命令行的方式安装

### IP 

raw.githubusercontent.com正确的 IP 

~~~
https://ipaddress.com/website/raw.githubusercontent.com
~~~

打开 add-onSSH & Web Terminal(关闭保护模式)
~~~
echo 185.199.108.133 raw.githubusercontent.com >> /etc/hosts

docker exec -i homeassistant bash -c "echo 185.199.108.133 raw.githubusercontent.com >> /etc/hosts"

~~~

下载自定义组件 HACS
~~~
wget -q -O - https://raw.githubusercontent.com/hacs/install/main/install | bash -
~~~


Home Assistant HAOS版如何安装HACS

https://blog.csdn.net/weixin_42672685/article/details/135087014

https://post.smzdm.com/p/a4dmmoqk/


## Home Assistant集成开发简明指南
https://bbs.hassbian.com/thread-25696-1-1.html


