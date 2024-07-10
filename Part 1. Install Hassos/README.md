
Configure Docker to use a proxy server

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

https://docs.docker.com/network/proxy/
