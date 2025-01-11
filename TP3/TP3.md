# TP3 MATHIS ALVAREZ
# Partie 1

```
PC1> ping 10.3.2.1

84 bytes from 10.3.2.1 icmp_seq=1 ttl=62 time=45.749 ms
84 bytes from 10.3.2.1 icmp_seq=2 ttl=62 time=27.530 ms
84 bytes from 10.3.2.1 icmp_seq=3 ttl=62 time=31.727 ms
84 bytes from 10.3.2.1 icmp_seq=4 ttl=62 time=30.063 ms
84 bytes from 10.3.2.1 icmp_seq=5 ttl=62 time=27.885 ms

```
```
R2#show arp
Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  10.3.12.1              19   c401.0517.0010  ARPA   FastEthernet0/0
Internet  10.3.12.2               -   c402.054b.0000  ARPA   FastEthernet0/0
Internet  10.3.2.1                2   0050.7966.6802  ARPA   FastEthernet0/1
Internet  10.3.2.254              -   c402.054b.0001  ARPA   FastEthernet0/1
R2#

routeur1#show arp
Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  10.3.12.1               -   c401.0517.0010  ARPA   FastEthernet1/0
Internet  10.3.12.2              18   c402.054b.0000  ARPA   FastEthernet1/0
Internet  10.3.1.1                2   0050.7966.6800  ARPA   FastEthernet0/0
Internet  10.3.1.254              -   c401.0517.0000  ARPA   FastEthernet0/0
routeur1#

routeur1#ping 1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 48/82/92 ms

```


```
PC1> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=57 time=42.712 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=57 time=43.879 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=57 time=38.573 ms
^C

R2(config)#ip route 0.0.0.0 0.0.0.0 10.3.12.1

PC3> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=56 time=60.546 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=56 time=46.149 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=56 time=58.611 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=56 time=59.904 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=56 time=49.328 ms
^C
PC3>

```

# Partie 2

```
PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.3.1.1/24
GATEWAY     : 255.255.255.0
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 20014
RHOST:PORT  : 127.0.0.1:20015
MTU         : 1500

PC1> ping 10.3.1.2

84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=2.780 ms
84 bytes from 10.3.1.2 icmp_seq=2 ttl=64 time=6.256 ms
84 bytes from 10.3.1.2 icmp_seq=3 ttl=64 time=8.367 ms
84 bytes from 10.3.1.2 icmp_seq=4 ttl=64 time=5.704 ms
^C
PC1>

PC3> show ip

NAME        : PC3[1]
IP/MASK     : 10.3.1.2/24
GATEWAY     : 255.255.255.0
DNS         :
MAC         : 00:50:79:66:68:02
LPORT       : 20018
RHOST:PORT  : 127.0.0.1:20019
MTU         : 1500

PC3> ping 10.3.1.1

84 bytes from 10.3.1.1 icmp_seq=1 ttl=64 time=4.868 ms
84 bytes from 10.3.1.1 icmp_seq=2 ttl=64 time=3.444 ms
84 bytes from 10.3.1.1 icmp_seq=3 ttl=64 time=2.833 ms
84 bytes from 10.3.1.1 icmp_seq=4 ttl=64 time=4.359 ms
84 bytes from 10.3.1.1 icmp_seq=5 ttl=64 time=4.148 ms
^C
PC3>

```

```
R1#ping 10.3.1.2

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.1.2, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 40/53/68 ms
R1#ping 10.3.1.2

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.1.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 32/44/64 ms


R1#ping 10.3.2.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.2.1, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 40/51/64 ms
R1#



PC1> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=53 time=42.294 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=53 time=28.898 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=53 time=29.137 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=53 time=29.979 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=53 time=32.631 ms

PC1>

PC3> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=53 time=39.200 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=53 time=31.434 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=53 time=28.309 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=53 time=37.842 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=53 time=26.301 ms
^C
PC3>


PC2> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=53 time=33.042 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=53 time=27.003 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=53 time=31.202 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=53 time=32.674 ms
^C
PC2>

R1#ping 1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 64/85/92 ms
R1#

```

# Partie 3

```
PC4> dhcp
DDORA IP 10.3.2.30/24 GW 10.3.2.254

PC4> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=57 time=39.019 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=57 time=37.732 ms

PC4> show ip

NAME        : PC4[1]
IP/MASK     : 10.3.2.30/24
GATEWAY     : 10.3.2.254
DNS         : 1.1.1.1
DHCP SERVER : 10.3.2.253
DHCP LEASE  : 478, 600/300/525
MAC         : 00:50:79:66:68:05
LPORT       : 20027
RHOST:PORT  : 127.0.0.1:20028
MTU         : 1500

PC4> ping efrei.fr
efrei.fr resolved to 51.255.68.208

84 bytes from 51.255.68.208 icmp_seq=1 ttl=53 time=41.092 ms
84 bytes from 51.255.68.208 icmp_seq=2 ttl=53 time=41.332 ms
84 bytes from 51.255.68.208 icmp_seq=3 ttl=53 time=45.556 ms
84 bytes from 51.255.68.208 icmp_seq=4 ttl=53 time=41.901 ms
^C
PC4>

PC4> show ip

NAME        : PC4[1]
IP/MASK     : 10.3.2.197/24
GATEWAY     : 10.3.2.254
DNS         : 10.3.3.1
DHCP SERVER : 10.3.2.253
DHCP LEASE  : 486, 494/247/432
MAC         : 00:50:79:66:68:03
LPORT       : 20027
RHOST:PORT  : 127.0.0.1:20028
MTU         : 1500

PC4>


```
