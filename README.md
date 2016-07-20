tsocks_dnsdirect
================
The project is forked from tsocks-1.84 patched by mac port.

My patch is made for tsocks failed to resolve host name when using iPhone tethering tools.

Why should I use it?
---------
If you can't ssh or use git through tethering, then use this.

This patch is intended for iPhone tethering tool hosted in
https://github.com/rickyzhang82/tethering . The patch overloads
gethostbyname, getaddrinfo and getipnodebyname by sending DNS
request directly to DNS server hosted on your iPhone.

This assumes that both your SOCKS proxy and DNS service host
in the same server. It resolved the outstanding issue that
OS X handle DNS configuration properly in ad-hoc network case.

How do I use it?
--------
1.Compile

run build.sh, assuming you can sudo

2.Configuration

In /etc/tsocks.conf,
```Python
tordns_enable = true
dns_direct_enable = true
server = ...your iPhone local wifi IP...
```
3.Disable SIP feature in Mac OS X.

You can't sockify ssh without disable SIP feature. Google it how.
