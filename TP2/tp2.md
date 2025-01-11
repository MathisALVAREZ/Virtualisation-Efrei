# TP2 MATHIS ALVAREZ B2CS-G1

# Routage
```
[kratox@dhcp network-scripts]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8c:cb:96 brd ff:ff:ff:ff:ff:ff
    inet 10.2.1.254/24 brd 10.2.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe8c:cb96/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a7:bf:e3 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.30/24 brd 192.168.56.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea7:bfe3/64 scope link
       valid_lft forever preferred_lft forever
4: enp0s9: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:81:ba:cd brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.153/24 brd 192.168.122.255 scope global dynamic noprefixroute enp0s9
       valid_lft 3566sec preferred_lft 3566sec
    inet6 fe80::78a6:de5e:9adf:a915/64 scope link noprefixroute
       valid_lft forever preferred_lft forever


[kratox@dhcp network-scripts]$ ping -c 4 google.com
PING google.com (216.58.215.46) 56(84) bytes of data.
64 bytes from par21s17-in-f14.1e100.net (216.58.215.46): icmp_seq=1 ttl=114 time=27.2 ms
64 bytes from par21s17-in-f14.1e100.net (216.58.215.46): icmp_seq=2 ttl=114 time=28.7 ms
^C
--- google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1003ms
rtt min/avg/max/mdev = 27.243/27.993/28.744/0.750 ms


[kratox@dhcp etc]$ sudo nano sysctl.conf
[kratox@dhcp etc]$ sudo sysctl -p
net.ipv4.ip_forward = 1
[kratox@dhcp etc]$ sudo firewall-cmd --add-masquerade
success
[kratox@dhcp etc]$ sudo firewall-cmd --add-masquerade --permanent
success
```

```

PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.2.1.1/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 20005
RHOST:PORT  : 127.0.0.1:20006
MTU         : 1500


PC1>
PC1> ping 10.2.1.254

84 bytes from 10.2.1.254 icmp_seq=1 ttl=64 time=11.510 ms
84 bytes from 10.2.1.254 icmp_seq=2 ttl=64 time=5.921 ms
84 bytes from 10.2.1.254 icmp_seq=3 ttl=64 time=11.958 ms
^C

PC1> trace 1.1.1.1
trace to 1.1.1.1, 8 hops max, press Ctrl+C to stop
 1   10.2.1.254   4.750 ms  4.771 ms  10.557 ms
 2   192.168.122.1   8.637 ms  12.414 ms  4.490 ms
 3   10.0.3.2   16.677 ms  12.275 ms  13.551 ms
 4     *  *  *
 5     *  *  *
 6     *  *  *
 7     *  *  *
^C 8     *

```

# Serveur DHCP

```
TYPE=Ethernet
BOOTPROTO=none
NAME=enp0s3
DEVICE=enp0s3
ONBOOT=yes
IPADDR=10.2.1.253
NETMASK=255.255.255.0
GATEWAY=10.2.1.254
DNS1=8.8.8.8
DNS2=8.8.4.4

default-lease-time 600;
max-lease-time 7200;
authoritative;

subnet 10.2.1.0 netmask 255.255.255.0 {
    range 10.2.1.100 10.2.1.200;
    option routers 10.2.1.254;
    option domain-name-servers 8.8.8.8, 1.1.1.1;
}


[root@dhcp dhcp]# systemctl status dhcpd
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset>
     Active: active (running) since Wed 2024-12-11 14:33:03 CET; 6s ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 1406 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 11099)
     Memory: 4.6M
        CPU: 34ms
     CGroup: /system.slice/dhcpd.service
             └─1406 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd>

Dec 11 14:33:03 dhcp.tp1.efrei dhcpd[1406]: ** Ignoring requests on enp0s8.>
Dec 11 14:33:03 dhcp.tp1.efrei dhcpd[1406]:    you want, please write a sub>
Dec 11 14:33:03 dhcp.tp1.efrei dhcpd[1406]:    in your dhcpd.conf file for >
Dec 11 14:33:03 dhcp.tp1.efrei dhcpd[1406]:    to which interface enp0s8 is>
Dec 11 14:33:03 dhcp.tp1.efrei dhcpd[1406]:
Dec 11 14:33:03 dhcp.tp1.efrei dhcpd[1406]: Listening on LPF/enp0s3/08:00:2>
Dec 11 14:33:03 dhcp.tp1.efrei dhcpd[1406]: Sending on   LPF/enp0s3/08:00:2>
Dec 11 14:33:03 dhcp.tp1.efrei dhcpd[1406]: Sending on   Socket/fallback/fa>
Dec 11 14:33:03 dhcp.tp1.efrei dhcpd[1406]: Server starting service.
Dec 11 14:33:03 dhcp.tp1.efrei systemd[1]: Started DHCPv4 Server Daemon.


```

```
[kratox@dhcp ~]$ nmcli connection show
NAME    UUID                                  TYPE      DEVICE
enp0s9  93d13955-e9e2-a6bd-df73-12e3c747f122  ethernet  enp0s9
lan     3c36b8c2-334b-57c7-91b6-4401f3489c69  ethernet  enp0s3
ssh     00cb8299-feb9-55b6-a378-3fdc720e0bc6  ethernet  enp0s8
lo      05314c02-88ca-4cbf-af18-4c23f824b18f  loopback  lo
[kratox@dhcp ~]$ sudo nmcli connection delete enp0s3
[sudo] password for kratox:
Error: unknown connection 'enp0s3'.
Error: cannot delete unknown connection(s): 'enp0s3'.


[kratox@dhcp ~]$ sudo nmcli connection delete lan
Connection 'lan' (3c36b8c2-334b-57c7-91b6-4401f3489c69) successfully deleted.


[kratox@dhcp ~]$ sudo systemctl restart NetworkManager.service


[kratox@dhcp ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8c:cb:96 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::3ff8:7a37:7121:4833/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a7:bf:e3 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.30/24 brd 192.168.56.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fea7:bfe3/64 scope link
       valid_lft forever preferred_lft forever
4: enp0s9: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:81:ba:cd brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.153/24 brd 192.168.122.255 scope global dynamic noprefixroute enp0s9
       valid_lft 3592sec preferred_lft 3592sec
    inet6 fe80::a00:27ff:fe81:bacd/64 scope link
       valid_lft forever preferred_lft forever


PC1> dhcp
DDORA IP 10.2.1.100/24 GW 10.2.1.254

PC1>

PC1> trace 1.1.1.1
trace to 1.1.1.1, 8 hops max, press Ctrl+C to stop
 1   10.2.1.254   7.944 ms  3.985 ms  7.037 ms
 2     *  *  *
 3   *10.2.1.254   78.790 ms (ICMP type:3, code:1, Destination host unreachable)

PC1>

```

# Les tables ARP

```
[kratox@dhcp ~]$ ip neigh show
129.250.35.250 dev enp0s3 FAILED
8.8.8.8 dev enp0s3 FAILED
192.168.122.1 dev enp0s9 lladdr 52:54:00:23:04:c2 STALE
188.165.49.6 dev enp0s3 FAILED
129.151.225.244 dev enp0s3 FAILED
5.39.80.51 dev enp0s3 FAILED
10.2.1.253 dev enp0s3 lladdr 08:00:27:03:ce:d1 STALE
82.67.62.62 dev enp0s3 FAILED
82.127.104.72 dev enp0s3 FAILED
1.1.1.1 dev enp0s3 FAILED
8.8.4.4 dev enp0s3 FAILED
10.2.1.100 dev enp0s3 lladdr 00:50:79:66:68:00 STALE
82.65.235.151 dev enp0s3 FAILED
188.213.31.235 dev enp0s3 FAILED
162.159.200.1 dev enp0s3 FAILED
192.168.56.1 dev enp0s8 lladdr 0a:00:27:00:00:05 DELAY
192.168.56.254 dev enp0s8 FAILED


[kratox@dhcp ~]$ sudo ip neigh del 10.2.1.253 dev enp0s3
[sudo] password for kratox:


[kratox@dhcp ~]$ ip neigh show
129.250.35.250 dev enp0s3 FAILED
8.8.8.8 dev enp0s3 FAILED
192.168.122.1 dev enp0s9 lladdr 52:54:00:23:04:c2 STALE
188.165.49.6 dev enp0s3 FAILED
129.151.225.244 dev enp0s3 FAILED
10.2.1.253 dev enp0s3 lladdr 08:00:27:03:ce:d1 REACHABLE
5.39.80.51 dev enp0s3 FAILED
82.67.62.62 dev enp0s3 FAILED
82.127.104.72 dev enp0s3 FAILED
1.1.1.1 dev enp0s3 FAILED
8.8.4.4 dev enp0s3 FAILED
10.2.1.100 dev enp0s3 lladdr 00:50:79:66:68:00 STALE
82.65.235.151 dev enp0s3 FAILED
188.213.31.235 dev enp0s3 FAILED
162.159.200.1 dev enp0s3 FAILED
192.168.56.1 dev enp0s8 lladdr 0a:00:27:00:00:05 DELAY
192.168.56.254 dev enp0s8 FAILED
```

# ARP Poisoning

```
┌──(kratox㉿kratox)-[~]
└─$ sudo arping -c 1 -S 10.2.1.129 -s AA:BB:CC:DD:EE:FF 10.2.1.100

ARPING 10.2.1.100
Timeout

--- 10.2.1.100 statistics ---
1 packets transmitted, 0 packets received, 100% unanswered (0 extra)

PC1> show arp

aa:bb:cc:dd:ee:ff  10.2.1.129 expires in 91 seconds

PC1>

```

```
┌──(kratox㉿kratox)-[~]
└─$ echo "1" | sudo tee /proc/sys/net/ipv4/ip_forward

1
                                                                                                                    
┌──(kratox㉿kratox)-[~]
└─$ cat /proc/sys/net/ipv4/ip_forward

1
                                                                                                                    




```