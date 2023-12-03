# IS-IS

### Задание:

Настроите IS-IS в ISP Триада.

1. R23 и R25 находятся в зоне 2222;
2. R24 находится в зоне 24;
3. R26 находится в зоне 26;
4. Настройка для IPv6 повторяет логику IPv4.

### Решение:

1. Настроим R23 и R25 в зоне 2222;
2. Настроим R24 в зоне 24;
3. Настроим R26 в зоне 26 и закоментируем все изменения.

### 1. Настроим R23 и R25 в зоне 2222:

Исследуемая схема описана [тут.](https://github.com/Pekep97/Labs/tree/main/Lab_04) Для упрощения понимания задублируем в этой работе только нужное:

### Исследуемая схема:

![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_07/Lab_07_IS-IS.png)

### Таблица адресного пространства:

|              |            |                 | *Триада*      |                       |             |              |             |                |
| **Hostname**     | **Interfaces** | **Description**     | **IPv4-address**  | **Mask**                  | **Gateway**     | **IPv6-address** | **IPv6-prefix** | **LLIPv6-address** |
| R23          | e0/0       | l3:to-AS-101    | 23.100.40.1   | 255.255.255.252 (/30) | -           | 2000:0:520:101::1   | /112        | fe80::2        |
|              | e0/1       | l3:to-R25       | 10.64.52.1    | 255.255.255.252 (/30) | -           | fd00:0:23:25::1     | /112        | fe80::1        |
|              | e0/2       | l3:to-R24       | 10.64.52.5    | 255.255.255.252 (/30) | -           | fd00:0:23:24::1     | /112        | fe80::1        |
| R24          | e0/0       | l3:to-AS-301    | 24.100.40.1   | 255.255.255.252 (/30) | -           | 2000:0:520:301::1   | /112        | fe80::2        |
|              | e0/1       | l3:to-R26       | 10.64.52.9    | 255.255.255.252 (/30) | -           | fd00:0:24:26::1     | /112        | fe80::2        |
|              | e0/2       | l3:to-R23       | 10.64.52.6    | 255.255.255.252 (/30) | -           | fd00:0:23:24::2     | /112        | fe80::2        |
|              | e0/3       | l3:to-AS-2042   | 24.100.40.5   | 255.255.255.252 (/30) | -           | 2000:0:520:2042::1  | /112        | fe80::2        |
| R25          | e0/0       | l3:to-R23       | 10.64.52.2    | 255.255.255.252 (/30) | -           | fd00:0:23:25::2     | /112        | fe80::2        |
|              | e0/1       | l3:to-LBTNG     | 1.1.1.2       | 255.255.255.252 (/30) | -           | 2000:0:520:1111::2  | /112        | fe80::2        |
|              | e0/2       | l3:to-R26       | 10.64.52.13   | 255.255.255.252 (/30) | -           | fd00:0:25:26::1     | /112        | fe80::2        |
|              | e0/3       | l3:to-CHKR      | 2.2.2.2       | 255.255.255.252 (/30) | -           | 2000:0:520:2222::2  | /112        | fe80::2        |
| R26          | e0/0       | l3:to-R24       | 10.64.52.10   | 255.255.255.252 (/30) | -           | fd00:0:24:26::2     | /112        | fe80::1        |
|              | e0/1       | l3:to-CHKR      | 3.3.3.2       | 255.255.255.252 (/30) | -           | 2000:0:520:3333::2  | /112        | fe80::1        |
|              | e0/2       | l3:to-R25       | 10.64.52.14   | 255.255.255.252 (/30) | -           | fd00:0:25:26::2     | /112        | fe80::1        |
|              | e0/3       | l3:to-AS-2042   | 26.100.40.1   | 255.255.255.252 (/30) | -           | 2000:0:2042:520::1  | /112        | fe80::1        |

Покажем пример настройки на маршрутизаторе R23:
```
R23#sh run | sec isis
 ip router isis AREA_2222
 ipv6 router isis AREA_2222
router isis AREA_2222
 net 49.2222.0000.0000.0023.00
 passive-interface Ethernet0/0
```

### 2. Настроим R24 в зоне 24:

Покажем настройки маршрутизатора R24:
```
R24#sh run | sec isis
 ip router isis AREA_24
 ipv6 router isis AREA_24
 ip router isis AREA_24
 ipv6 router isis AREA_24
router isis AREA_24
 net 49.0024.0000.0000.0024.00
 is-type level-2-only
 passive-interface Ethernet0/0
 passive-interface Ethernet0/3
```

### 3. Настроим R26 в зоне 26 и закоментируем все изменения:


Покажем настройки маршрутизатора R26:
```
R26#sh run | sec isis
 ip router isis AREA_26
 ipv6 router isis AREA_26
 ip router isis AREA_26
 ipv6 router isis AREA_26
router isis AREA_26
 net 49.0026.0000.0000.0026.00
 is-type level-2-only
 passive-interface Ethernet0/1
 passive-interface Ethernet0/3
```

- Для подтверждения правильности настроек покажем таблицу маршрутизации на маршрутизаторе R26:

*IPv4*
```
R26#sh ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       a - application route
       + - replicated route, % - next hop override

Gateway of last resort is not set

      1.0.0.0/30 is subnetted, 1 subnets
i L2     1.1.1.0 [115/10] via 10.64.52.13, 00:01:58, Ethernet0/2
      2.0.0.0/30 is subnetted, 1 subnets
i L2     2.2.2.0 [115/10] via 10.64.52.13, 00:01:58, Ethernet0/2
      3.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        3.3.3.0/30 is directly connected, Ethernet0/1
L        3.3.3.2/32 is directly connected, Ethernet0/1
      10.0.0.0/8 is variably subnetted, 7 subnets, 3 masks
S        10.58.10.0/24 [1/0] via 3.3.3.1
i L2     10.64.52.0/30 [115/20] via 10.64.52.13, 00:01:58, Ethernet0/2
i L2     10.64.52.4/30 [115/20] via 10.64.52.9, 00:05:23, Ethernet0/0
C        10.64.52.8/30 is directly connected, Ethernet0/0
L        10.64.52.10/32 is directly connected, Ethernet0/0
C        10.64.52.12/30 is directly connected, Ethernet0/2
L        10.64.52.14/32 is directly connected, Ethernet0/2
      23.0.0.0/30 is subnetted, 1 subnets
i L2     23.100.40.0 [115/20] via 10.64.52.13, 00:01:58, Ethernet0/2
                     [115/20] via 10.64.52.9, 00:01:58, Ethernet0/0
      24.0.0.0/30 is subnetted, 2 subnets
i L2     24.100.40.0 [115/10] via 10.64.52.9, 00:05:23, Ethernet0/0
i L2     24.100.40.4 [115/10] via 10.64.52.9, 00:05:23, Ethernet0/0
      26.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        26.100.40.0/30 is directly connected, Ethernet0/3
L        26.100.40.1/32 is directly connected, Ethernet0/3
S     192.168.100.0/24 [1/0] via 3.3.3.1
```

*IPv6*
```
R26#sh ipv6 route
IPv6 Routing Table - default - 15 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, HA - Home Agent, MR - Mobile Router, R - RIP
       H - NHRP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, NM - NEMO
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, la - LISP alt
       lr - LISP site-registrations, ld - LISP dyn-eid, a - Application
I2  2000:0:520:301::/112 [115/10]
     via FE80::2, Ethernet0/0
I2  2000:0:520:1111::/112 [115/10]
     via FE80::2, Ethernet0/2
I2  2000:0:520:2042::/112 [115/10]
     via FE80::2, Ethernet0/0
I2  2000:0:520:2222::/112 [115/10]
     via FE80::2, Ethernet0/2
C   2000:0:520:3333::/112 [0/0]
     via Ethernet0/1, directly connected
L   2000:0:520:3333::2/128 [0/0]
     via Ethernet0/1, receive
C   2000:0:2042:520::/112 [0/0]
     via Ethernet0/3, directly connected
L   2000:0:2042:520::1/128 [0/0]
     via Ethernet0/3, receive
I2  FD00:0:23:24::/112 [115/20]
     via FE80::2, Ethernet0/0
I2  FD00:0:23:25::/112 [115/20]
     via FE80::2, Ethernet0/2
C   FD00:0:24:26::/112 [0/0]
     via Ethernet0/0, directly connected
L   FD00:0:24:26::2/128 [0/0]
     via Ethernet0/0, receive
C   FD00:0:25:26::/112 [0/0]
     via Ethernet0/2, directly connected
L   FD00:0:25:26::2/128 [0/0]
     via Ethernet0/2, receive
L   FF00::/8 [0/0]
     via Null0, receive
```

Все изменения приведены [здесь.]()
