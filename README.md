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

In /etc/tsocks.conf, fill in your iPhone IP socks 5 server IP, port and socks version and set the DNS flags to true.

```
# This is the configuration for libtsocks (transparent socks)
# Lines beginning with # and blank lines are ignored
#
# This sample configuration shows the simplest (and most common) use of
# tsocks. This is a basic LAN, this machine can access anything on the
# local ethernet (192.168.0.*) but anything else has to use the SOCKS version
# 4 server on the firewall. Further details can be found in the man pages,
# tsocks(8) and tsocks.conf(5) and a more complex example is presented in
# tsocks.conf.complex.example

# We can access 192.168.0.* directly
local = 192.168.100.0/255.255.255.0

# Otherwise we use the server
server = 192.168.100.2
server_type = 5
server_port = 3128
tordns_enable = true
dns_direct_enable = true
```

