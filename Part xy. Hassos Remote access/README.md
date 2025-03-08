
The fix has 3 steps

1. Check configuration->basic->log for reverse proxy error. Note the IP address in the error message. if you don’t have it, then you have a different problem.

2. Edit the configuration.yaml file
~~~
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - XXX.XXX.XXX.XXX # Add the IP address of the proxy server
~~~

3. Restart your Home Assistant server


demo
~~~
# Cloudflare setting to unlock reverse proxy
http:
   use_x_forwarded_for: true 
   trusted proxies:
	- 172.30.33.0/24
	- 103.21.244.0/22
	- 103.22.200.0/22
	- 103.31.4.0/22
	- 104.16.0.0/13
	- 104.24.0.0/14
	- 108.162.192.0/18
	- 131.0.72.0/22
	- 141.101.64.0/18
	- 162.158.0.0/15
	- 172.64.0.0/13
	- 173.245.48.0/20
	- 188.114.96.0/20
	- 190.93.240.0/20
	- 197.234.240.0/22
	- 198.41.128.0/17
~~~