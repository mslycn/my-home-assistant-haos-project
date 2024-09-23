
/etc/hosts

~~~
hosts文件是linux系统中负责ip地址与域名快速解析的文件
以ASCII格式保存在/etc目录下
文件名为hosts(不同的linux版本，文件也可能不同，比如Debian的对应文件是/etc/hostname。)
hosts文件包含了ip地址和主机名之间的映射，包括主机名的别名(在没有域名服务器的情况下，系统上的所有网络程序都通过查询该文件来解析对应于某个主机名的ip地址，否则就需要使用DNS服务程序来解决。)
通常可以将常用的域名和ip地址映射加入到hosts文件中，实现快速方便的访问

~~~

优先级：dns缓存>hosts>dns服务


~~~

PRETTY_NAME="Debian GNU/Linux 12 (bookworm)"
NAME="Debian GNU/Linux"
VERSION_ID="12"
VERSION="12 (bookworm)"
VERSION_CODENAME=bookworm
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"

~~~


raspberrypi's /etc/hosts

~~~
127.0.0.1	localhost
::1		localhost ip6-localhost ip6-loopback
ff02::1		ip6-allnodes
ff02::2		ip6-allrouters

127.0.1.1		raspberrypi
185.199.108.133 raw.githubusercontent.com
140.82.114.4 github.com
~~~
