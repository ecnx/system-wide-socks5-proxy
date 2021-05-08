Purpose
-------
To make every program on Desktop connect to ports 80 and 443 via proxy.

Programs
--------
Two programs axproxy and vsocks available here will be needed

How to?
-------
Setup plain Socks-5 server on VPS:
```
axproxy 0.0.0.0:8080 # listen on any-ipv4:8080
```
Setup proxy gateway on Desktop:
```
vsocks 0.0.0.0:8082 <vps-ipv4>:8080
```
Configure iptables:
```
iptables -F
iptables -t nat -F
iptables -t nat -A OUTPUT -p tcp --dport 80 -j DNAT --to-destination 127.0.0.1:8082
```
Finally check results:
```
curl http://ipinfo.io/json -o -
```

Encryped Socks-5 connection
---------------------------
See sockscrypt (another project here) for more information.

What about DNS?
---------------
Try using DNS over TLS (for example with stubby) and tunnel port 53 too.
Otherwise DNS traffic will not go through the Socks-5 Proxy.
