# tsocks_dnsdirect
The project is forked from tsocks-1.84 patched by mac port.

My patch fixed the tsocks bug that failed to resolve the host name when using iPhone tethering tools.

## Why should I use it?

If you can't ssh or use git through tethering, then use this.

This patch is intended for iPhone tethering tool hosted in
https://github.com/rickyzhang82/tethering . The patch overloads
BSD function `gethostbyname`, `getaddrinfo` and `getipnodebyname` 
by sending the DNS request directly to the DNS server hosted on your iPhone.

This assumes that both SOCKS proxy and DNS server host
in the same server. It resolved the outstanding issue that
OS X handle DNS configuration properly in ad-hoc network case.

## How do I use it?

### Step 1. Compile

run `build.sh`. It requires you can sudo to install.

### Step 2. Configuration

In /etc/tsocks.conf, fill in your iPhone socks 5 server IP, port and socks version and set the DNS flags to true.

Below is an example where the socks 5 server in the tethering app listens to IP `192.168.100.2` and port `3128`.

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
### Step 3. sockify your app

You can either use `tsocks ahead you command` or use `tsocks on/off`. 

Here is an example. I run git fetch on my Mac Studio through my iPhone. 

```
[Ricky@ms:tethering](master)$ tsocks git fetch origin
remote: Enumerating objects: 37, done.
remote: Counting objects: 100% (37/37), done.
remote: Compressing objects: 100% (26/26), done.
remote: Total 37 (delta 14), reused 33 (delta 10), pack-reused 0
Unpacking objects: 100% (37/37), 15.40 KiB | 508.00 KiB/s, done.
From github.com:rickyzhang82/tethering
   53343f3..c7928fa  master     -> origin/master
 * [new branch]      dev-ci     -> origin/dev-ci
 * [new tag]         V1.8       -> V1.8
```
