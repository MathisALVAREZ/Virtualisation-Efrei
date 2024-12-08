# TP1

```
PC2> show ip

NAME        : PC2[1]
IP/MASK     : 10.1.1.2/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:01
LPORT       : 20004
RHOST:PORT  : 127.0.0.1:20005
MTU         : 1500

PC2> ip 10.1.1.2/24
Checking for duplicate address...
PC2 : 10.1.1.2 255.255.255.0

```
```
PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.1.1.1/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 20002
RHOST:PORT  : 127.0.0.1:20003
MTU         : 1500


PC1> ip 10.1.1.1/24
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0

```

```
PC1> ping 10.1.1.2/24

84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=2.095 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=0.959 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=3.835 ms

PC1>

```

```
PC2> ping 10.1.1.1/24

84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=4.219 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=0.854 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=4.324 ms
84 bytes from 10.1.1.1 icmp_seq=4 ttl=64 time=0.319 ms

PC2>
```

```
PC2> show arp

00:50:79:66:68:00  10.1.1.1 expires in 118 seconds

PC2>
PC2>
```
```
VPCS> show ip

NAME        : VPCS[1]
IP/MASK     : 0.0.0.0/0
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 20002
RHOST:PORT  : 127.0.0.1:20003
MTU         : 1500

VPCS> ip 10.1.1.1/24
Checking for duplicate address...
VPCS : 10.1.1.1 255.255.255.0



VPCS> ip 10.1.1.2/24
Checking for duplicate address...
VPCS : 10.1.1.2 255.255.255.0

VPCS> show ip

NAME        : VPCS[1]
IP/MASK     : 10.1.1.2/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:01
LPORT       : 20004
RHOST:PORT  : 127.0.0.1:20005
MTU         : 1500




VPCS> show ip

NAME        : VPCS[1]
IP/MASK     : 0.0.0.0/0
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:02
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:20001
MTU         : 1500

VPCS> ip 10.1.1.3/24
Checking for duplicate address...
VPCS : 10.1.1.3 255.255.255.0

```

```
VPCS>
VPCS> ping 10.1.1.2/24

84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=5.524 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=5.886 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=1.845 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=1.931 ms
^C
VPCS>


VPCS> ping 10.1.1.3/24

84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=2.998 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=1.948 ms
84 bytes from 10.1.1.3 icmp_seq=3 ttl=64 time=3.051 ms
84 bytes from 10.1.1.3 icmp_seq=4 ttl=64 time=2.093 ms
^C
VPCS>


VPCS> ping 10.1.1.3/24

84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=0.653 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=0.969 ms
84 bytes from 10.1.1.3 icmp_seq=3 ttl=64 time=0.973 ms
84 bytes from 10.1.1.3 icmp_seq=4 ttl=64 time=1.008 ms
84 bytes from 10.1.1.3 icmp_seq=5 ttl=64 time=0.391 ms

VPCS>

```
```
[root@localhost etc]# ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=60 time=24.7 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=60 time=22.6 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=60 time=21.1 ms
^C
--- 1.1.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2006ms
rtt min/avg/max/mdev = 21.058/22.772/24.673/1.481 ms
[root@localhost etc]#
```

```
[root@localhost ~]# sudo dnf install dhcp-server
Last metadata expiration check: 0:30:20 ago on Fri Nov 15 10:15:57 2024.
Dependencies resolved.
============================================================================================================================================================
 Package                               Architecture                     Version                                      Repository                        Size
============================================================================================================================================================
Installing:
 dhcp-server                           x86_64                           12:4.4.2-19.b1.el9                           baseos                           1.2 M
Installing dependencies:
 dhcp-common                           noarch                           12:4.4.2-19.b1.el9                           baseos                           128 k

Transaction Summary
============================================================================================================================================================
Install  2 Packages

Total download size: 1.3 M
Installed size: 4.2 M

```

```
[root@localhost dhcp]# nano dhcpd.conf
[root@localhost dhcp]# cat dhcpd.conf
# default lease time
default-lease-time 600;
# max lease time
max-lease-time 7200;
# this DHCP server to be declared valid
authoritative;

subnet 10.1.1.253 netmask 255.255.255.0 {
    # specify the range of lease IP address
    range dynamic-bootp 10.1.1.10 10.1.1.50;
    # specify broadcast address
    option broadcast-address 10.0.0.255;
    # specify gateway
    option routers 10.0.0.1;
}
[root@localhost dhcp]#
```
```
[root@localhost system-connections]# ip addr add 10.1.1.1/24 dev enp0s9
[root@localhost system-connections]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:40:86:ef brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.102/24 brd 192.168.56.255 scope global dynamic noprefixroute enp0s8
       valid_lft 534sec preferred_lft 534sec
    inet6 fe80::eaa8:1979:ee81:490d/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s9: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:1e:6d:60 brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.1/24 scope global enp0s9
       valid_lft forever preferred_lft forever
    inet6 fe80::4cd3:8b6f:ee7:83c2/64 scope link noprefixroute
       valid_lft forever preferred_lft forever



[root@localhost system-connections]# systemctl restart dhcp
Failed to restart dhcp.service: Unit dhcp.service not found.
[root@localhost system-connections]# sudo systemctl restart dhcpd
[root@localhost system-connections]# systemctl start dhcpd.service
[root@localhost system-connections]# systemctl status dhcpd.service
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; disabled; preset: disabled)
     Active: active (running) since Fri 2024-11-15 12:43:34 CET; 23s ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 2046 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 11112)
     Memory: 4.5M
        CPU: 24ms
     CGroup: /system.slice/dhcpd.service
             └─2046 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dhcpd --no-pid

Nov 15 12:43:34 localhost.localdomain systemd[1]: Started DHCPv4 Server Daemon.
Nov 15 12:43:37 localhost.localdomain dhcpd[2046]: DHCPDISCOVER from 08:00:27:1e:6d:60 via enp0s9
Nov 15 12:43:37 localhost.localdomain dhcpd[2046]: icmp_echorequest 10.1.1.10: Network is unreachable
Nov 15 12:43:38 localhost.localdomain dhcpd[2046]: DHCPOFFER on 10.1.1.10 to 08:00:27:1e:6d:60 via enp0s9
Nov 15 12:43:40 localhost.localdomain dhcpd[2046]: DHCPDISCOVER from 08:00:27:1e:6d:60 via enp0s9
Nov 15 12:43:40 localhost.localdomain dhcpd[2046]: DHCPOFFER on 10.1.1.10 to 08:00:27:1e:6d:60 via enp0s9
Nov 15 12:43:44 localhost.localdomain dhcpd[2046]: DHCPDISCOVER from 08:00:27:1e:6d:60 via enp0s9
Nov 15 12:43:44 localhost.localdomain dhcpd[2046]: DHCPOFFER on 10.1.1.10 to 08:00:27:1e:6d:60 via enp0s9
Nov 15 12:43:53 localhost.localdomain dhcpd[2046]: DHCPDISCOVER from 08:00:27:1e:6d:60 via enp0s9
Nov 15 12:43:53 localhost.localdomain dhcpd[2046]: DHCPOFFER on 10.1.1.10 to 08:00:27:1e:6d:60 via enp0s9
[root@localhost system-connections]#
```

```
VPCS> dhcp
DDORA
VPCS> show ip IP 10.1.1.11/24

NAME        : VPCS[1]
IP/MASK     : 10.1.1.11/24
GATEWAY     : 0.0.0.0
DNS         :
DHCP SERVER : 10.1.1.1
DHCP LEASE  : 596, 600/300/525
MAC         : 00:50:79:66:68:01
LPORT       : 20004
RHOST:PORT  : 127.0.0.1:20005
MTU         : 1500

VPCS>

VPCS> dhcp
DDORA
VPCS> show ip IP 10.1.1.12/24

NAME        : VPCS[1]
IP/MASK     : 10.1.1.12/24
GATEWAY     : 0.0.0.0
DNS         :
DHCP SERVER : 10.1.1.1
DHCP LEASE  : 572, 600/300/525
MAC         : 00:50:79:66:68:02
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:20001
MTU         : 1500

VPCS>


```
```
sudo apt install dnsmasq -y

sudo nano /etc/dnsmasq.conf

interface=enth0
dhcp-range=10.1.1.210,10.1.1.250,255.255.255.0,12h
dhcp-option=3,10.1.1.1    # Routeur par défaut
dhcp-option=6,8.8.8.8     # Serveur DNS (Google DNS)
no-resolv                 # Désactive la fonction DNS
log-queries               # (Optionnel) Log des requêtes DHCP
log-dhcp                  # (Optionnel) Log des réponses DHCP

┌──(kratox㉿kratox)-[~]
└─$ sudo systemctl start dnsmasq
                                                                                                                                                                                                                                           
┌──(kratox㉿kratox)-[~]
└─$ sudo systemctl status dnsmasq

```

```
[kratox@dhcp ~]$ sudo systemctl stop dhcpd

┌──(kratox㉿kratox)-[~]
└─$ sudo systemctl status ssh
○ ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: disabled)
     Active: inactive (dead)
       Docs: man:sshd(8)
             man:sshd_config(5)

┌──(kratox㉿kratox)-[~]
└─$ sudo systemctl start ssh 

```
```
──(kratox㉿kratox)-[/etc]
└─$ sudo systemctl status  dnsmasq 
● dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server
     Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; enabled; preset: disabled)
     Active: active (running) since Sun 2024-12-08 22:26:08 CET; 2s ago
 Invocation: 98e1c71874de456b8949b09f26219857
    Process: 8370 ExecStartPre=/usr/share/dnsmasq/systemd-helper checkconfig (code=exited, status=0/SUCCESS)
    Process: 8376 ExecStart=/usr/share/dnsmasq/systemd-helper exec (code=exited, status=0/SUCCESS)
    Process: 8383 ExecStartPost=/usr/share/dnsmasq/systemd-helper start-resolvconf (code=exited, status=0/SUCCESS)
   Main PID: 8381 (dnsmasq)
      Tasks: 1 (limit: 4546)
     Memory: 672K (peak: 2.2M)
        CPU: 32ms
     CGroup: /system.slice/dnsmasq.service
             └─8381 /usr/sbin/dnsmasq -x /run/dnsmasq/dnsmasq.pid -u dnsmasq -7 /etc/dnsmasq.d,.dpkg-dist,.dpkg-old,.dpkg-new --local-s>

Dec 08 22:26:08 kratox systemd[1]: Starting dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server...
Dec 08 22:26:08 kratox dnsmasq[8381]: started, version 2.90 cachesize 150
Dec 08 22:26:08 kratox dnsmasq[8381]: compile time options: IPv6 GNU-getopt DBus no-UBus i18n IDN2 DHCP DHCPv6 no-Lua TFTP conntrack ip>
Dec 08 22:26:08 kratox dnsmasq[8381]: warning: no upstream servers configured
Dec 08 22:26:08 kratox dnsmasq-dhcp[8381]: DHCP, IP range 10.1.1.210 -- 10.1.1.250, lease time 12h
Dec 08 22:26:08 kratox dnsmasq[8381]: read /etc/hosts - 8 names
Dec 08 22:26:08 kratox systemd[1]: Started dnsmasq.service - dnsmasq - A lightweight DHCP and caching DNS server.

```
```

PC2> ip dhcp
DDORA IP 10.1.1.247/24 GW 10.1.1.1

PC2>
```

