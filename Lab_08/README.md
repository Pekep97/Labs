# EIGRP

### Задание:

1. В офисе С.-Петербург настроить EIGRP;
2. R32 получает только маршрут по умолчанию;
3. R16-17 анонсируют только суммарные префиксы;
4. Использовать EIGRP named-mode для настройки сети;
5. Настройка осуществляется одновременно для IPv4 и IPv6.

### Решение: 

1. [Настроим маршрутизатор R32 так, чтобы он получал только маршрут по умолчанию;](https://github.com/Pekep97/Labs/blob/main/Lab_08/README.md#1-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80-r32-%D1%82%D0%B0%D0%BA-%D1%87%D1%82%D0%BE%D0%B1%D1%8B-%D0%BE%D0%BD-%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B0%D0%BB-%D1%82%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82-%D0%BF%D0%BE-%D1%83%D0%BC%D0%BE%D0%BB%D1%87%D0%B0%D0%BD%D0%B8%D1%8E)
2. [Настроим маршрутизаторы R16-17 так, чтобы они анонсировали только суммарные префиксы и задокументируем все изменения.](https://github.com/Pekep97/Labs/blob/main/Lab_08/README.md#2-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80%D1%8B-r16-17-%D1%82%D0%B0%D0%BA-%D1%87%D1%82%D0%BE%D0%B1%D1%8B-%D0%BE%D0%BD%D0%B8-%D0%B0%D0%BD%D0%BE%D0%BD%D1%81%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BB%D0%B8-%D1%82%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE-%D1%81%D1%83%D0%BC%D0%BC%D0%B0%D1%80%D0%BD%D1%8B%D0%B5-%D0%BF%D1%80%D0%B5%D1%84%D0%B8%D0%BA%D1%81%D1%8B-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)

### 1. Настроим маршрутизатор R32 так, чтобы он получал только маршрут по умолчанию:

- Исследуемая схема описана [тут.](https://github.com/Pekep97/Labs/tree/main/Lab_04) Для упрощения понимания задублируем в этой работе только нужное:

### Исследуемая схема:

![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_08/Lab_08_EIGRP.jpg)

### Таблица адресного пространства:

|              |            |                | *С.-Петербург*|                       |             |                     |             |                |
|--------------|------------|----------------|---------------|-----------------------|-------------|---------------------|-------------|----------------|
| **Hostname** |**Interfaces**|**Description**|**IPv4-address**|**Mask**             |**Gateway**  |**IPv6-address**     |**IPv6-prefix**|**LLIPv6-address**|
| R16          | e0/0.200   | MANAGEMENT_SPB | 10.58.200.2   | 255.255.255.0 (/24)   | -           | fd00:10:58:200::1   | /64         | fe80::1        |
|              | e0/2.20    | DHCP_SPB       | 192.168.20.2  | 255.255.255.0 (/24)   | -           | fd00:192:168:20::1  | /64         | fe80::1        |
|              | e0/1       | l3:to-R18      | 10.64.20.6    | 255.255.255.252 (/30) | -           | fd00:0:16:18::2     | /112        | fe80::2        |
|              | e0/3       | l3:to-R32      | 10.64.20.9    | 255.255.255.252 (/30) | -           | fd00:0:16:32::1     | /112        | fe80::1        |
| R17          | e0/0.200   | MANAGEMENT_SPB | 10.58.200.3   | 255.255.255.0 (/24)   | -           | fd00:10:58:200::1   | /64         | fe80::1        |
|              | e0/2.20    | DHCP_SPB       | 192.168.20.3  | 255.255.255.0 (/24)   | -           | fd00:192:168:200::1 | /64         | fe80::1        |
|              | e0/1       | l3:to-R18      | 10.64.20.2    | 255.255.255.252 (/30) | -           | fd00:0:17:18::2     | /112        | fe80::2        |
| R18          | e0/0       | l3:to-R16      | 10.64.20.5    | 255.255.255.252 (/30) | -           | fd00:0:16:18::1     | /112        | fe80::1        |
|              | e0/1       | l3:to-R17      | 10.64.20.1    | 255.255.255.252 (/30) | -           | fd00:0:17:18::1     | /112        | fe80::1        |
|              | e0/2       | l3:to-AS-520   | 24.100.40.6   | 255.255.255.252 (/30) | -           | 2000:0:520:2042::2  | /112        | fe80::1        |
|              | e0/3       | l3:to-AS-520   | 26.100.40.2   | 255.255.255.252 (/30) | -           | 2000:0:2042:520::2  | /112        | fe80::2        |
| R32          | e0/0       | l3:to-R16      | 10.64.20.10   | 255.255.255.252 (/30) | -           | fd00:0:16:32::2     | /112        | fe80::2        |
| VRRP_R16+R17 | -          | MANAGEMENT_SPB | 10.58.200.1   | 255.255.255.0 (/24)   | -           | -                   | -           | -              |
|              | -          | DHCP_SPB       | 192.168.20.1  | 255.255.255.0 (/24)   | -           | -                   | -           | -              |
| SW9          | VLAN200    | MANAGEMENT_SPB | 10.58.200.109 | 255.255.255.0 (/24)   | 10.58.200.1 | fd00:10:58:200::9   | /64         | fe80::9        |
| SW10         | VLAN200    | MANAGEMENT_SPB | 10.58.200.110 | 255.255.255.0 (/24)   | 10.58.200.1 | fd00:10:58:200::10  | /64         | fe80::10       |
| VPC          | NIC        | -              | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |
| VPC8         | NIC        | -              | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |


- Для реализации выполнения условия, требуется:
  * создать *prefix-list R32* на маршрутизаторе R16;
  * анонсировать маршрут по умолчанию в протокол EIGRP, сделаем это на маршрутизаторе R18;
 
- Покажем конфигурацию на R16, R18:

*R16_IPv4*
```
R16#sh run | sec eigrp
 ipv6 eigrp 1
router eigrp NAMED
 !
 address-family ipv4 unicast autonomous-system 1
  !
  af-interface Ethernet0/1
   no next-hop-self
  exit-af-interface
  !
  topology base
   auto-summary
   distribute-list prefix R32 out Ethernet0/3
  exit-af-topology
  network 10.58.200.0 0.0.0.255
  network 10.64.20.4 0.0.0.3
  network 10.64.20.8 0.0.0.3
  network 192.168.20.0
  eigrp router-id 16.16.16.16
 exit-address-family
 !
 ip prefix-list R32 seq 10 permit 0.0.0.0/0
```

*R16_IPv6*
```
router eigrp NAMED_v6
 !
 address-family ipv6 unicast autonomous-system 1
  !
  topology base
   distribute-list prefix-list R32_v6 out Ethernet0/3
  exit-af-topology
  eigrp router-id 16.16.16.16
 exit-address-family
!
ipv6 prefix-list R32_v6 seq 5 permit ::/0
```

*R18_IPv4*
```
R18#sh run | section eigrp
router eigrp NAMED
 !
 address-family ipv4 unicast autonomous-system 1
  !
  af-interface Ethernet0/0
   summary-address 0.0.0.0 0.0.0.0
  exit-af-interface
  !
  af-interface Ethernet0/1
   summary-address 0.0.0.0 0.0.0.0
  exit-af-interface
  !
  topology base
  exit-af-topology
  network 10.64.20.0 0.0.0.3
  eigrp router-id 18.18.18.18
 exit-address-family
```

*R18_IPv6*
```
router eigrp NAMED_v6
 !
 address-family ipv6 unicast autonomous-system 1
  !
  af-interface default
   shutdown
  exit-af-interface
  !
  af-interface Ethernet0/2
   passive-interface
  exit-af-interface
  !
  af-interface Ethernet0/3
   passive-interface
  exit-af-interface
  !
  af-interface Ethernet0/0
   summary-address ::/0
   no shutdown
  exit-af-interface
  !
  af-interface Ethernet0/1
   summary-address ::/0
   no shutdown
  exit-af-interface
  !
  topology base
  exit-af-topology
  eigrp router-id 18.18.18.18
 exit-address-family
```

- покажем таблицу маршрутизации на R32:
```
R32#sh ip route eigrp
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       a - application route
       + - replicated route, % - next hop override

Gateway of last resort is 10.64.20.9 to network 0.0.0.0

D*    0.0.0.0/0 [90/1536000] via 10.64.20.9, 01:02:15, Ethernet0/0
```

- как видим, маршрутизатор получает только один маршрут по умолчанию.

### 2. Настроим маршрутизаторы R16-17 так, чтобы они анонсировали только суммарные префиксы и задокументируем все изменения:

- на маршрутизаторах R16-17 для решения поставленной задачи требуется прописать команду *auto-summary* в режиме настройки EIGRP (суммаризация работает только в версии IPv4)
- покажем, для примера, конфигурацию R17:
```
R17#sh run | sec eigrp
router eigrp NAMED
 !
 address-family ipv4 unicast autonomous-system 1
  !
  topology base
   auto-summary
  exit-af-topology
  network 10.0.0.0
  network 10.58.20.0 0.0.0.255
  network 192.168.20.0
  eigrp router-id 17.17.17.17
 exit-address-family
router eigrp NAMED_v6
 !
 address-family ipv6 unicast autonomous-system 1
  !
  af-interface default
   shutdown
  exit-af-interface
  !
  af-interface Ethernet0/1
   no shutdown
  exit-af-interface
  !
  af-interface Ethernet0/0.200
   no shutdown
  exit-af-interface
  !
  af-interface Ethernet0/2.20
   no shutdown
  exit-af-interface
  !
  topology base
  exit-af-topology
  eigrp router-id 17.17.17.17
 exit-address-family
```

- покажем что суммаризация работает командой *show ip protocols* на R17:
```
R17#sh ip protocols
*** IP Routing is NSF aware ***

Routing Protocol is "application"
  Sending updates every 0 seconds
  Invalid after 0 seconds, hold down 0, flushed after 0
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Maximum path: 32
  Routing for Networks:
  Routing Information Sources:
    Gateway         Distance      Last Update
  Distance: (default is 4)

Routing Protocol is "eigrp 1"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Default networks flagged in outgoing updates
  Default networks accepted from incoming updates
  EIGRP-IPv4 VR(NAMED) Address-Family Protocol for AS(1)
    Metric weight K1=1, K2=0, K3=1, K4=0, K5=0 K6=0
    Metric rib-scale 128
    Metric version 64bit
    NSF-aware route hold timer is 240
    Router-ID: 17.17.17.17
    Topology : 0 (base)
      Active Timer: 3 min
      Distance: internal 90 external 170
      Maximum path: 4
      Maximum hopcount 100
      Maximum metric variance 1

  !!!!!!!!!!!!!!!!!!!!!Automatic Summarization: enabled!!!!!!!!!!!!!!!!!!!!!!!!!!!
    192.168.20.0/24 for Et0/0.200, Et0/1
    10.0.0.0/8 for Et0/2.20
      Summarizing 4 components with metric 131072000
  Maximum path: 4
  Routing for Networks:
    10.58.20.0/24
    10.0.0.0
    192.168.20.0
  Routing Information Sources:
    Gateway         Distance      Last Update
    10.64.20.1            90      00:39:22
    192.168.20.2          90      00:39:22
    10.58.200.2           90      00:39:22
  Distance: internal 90 external 170
```

- настройка маршрутизатора R18 выполнялась с учетом того, что это пограничный маршрутизатор, покажем ее:

*R18_IPv4*
```
R18#sh run | sec eigrp
router eigrp NAMED
 !
 address-family ipv4 unicast autonomous-system 1
  !
  af-interface Ethernet0/0
   summary-address 0.0.0.0 0.0.0.0
  exit-af-interface
  !
  af-interface Ethernet0/1
   summary-address 0.0.0.0 0.0.0.0
  exit-af-interface
  !
  topology base
  exit-af-topology
  network 10.64.20.0 0.0.0.3
  eigrp router-id 18.18.18.18
 exit-address-family
```

*R18_IPv6
```
router eigrp NAMED_v6
 !
 address-family ipv6 unicast autonomous-system 1
  !
  af-interface default
   shutdown
  exit-af-interface
  !
  af-interface Ethernet0/2
   passive-interface
  exit-af-interface
  !
  af-interface Ethernet0/3
   passive-interface
  exit-af-interface
  !
  af-interface Ethernet0/0
   summary-address ::/0
   no shutdown
  exit-af-interface
  !
  af-interface Ethernet0/1
   summary-address ::/0
   no shutdown
  exit-af-interface
  !
  topology base
  exit-af-topology
  eigrp router-id 18.18.18.18
 exit-address-family
```

- проверим связность сети утилитой ***ping*** от маршрутизатора R17 до маршрутизатора R32:


*IPv4*
```
R17#ping 10.64.20.10
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.64.20.10, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/2 ms
```

*IPv6*
```
R17#ping FD00:0:16:32::2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to FD00:0:16:32::2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
```

Все изменения задокументрованы [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_08/Configs)
