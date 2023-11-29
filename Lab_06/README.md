# OSPF 

### Задание:

Настроить OSPF в офисе Москва:

1. Маршрутизаторы R14-R15 находятся в зоне 0 - backbone;
2. Маршрутизаторы R12-R13 находятся в зоне 10. Дополнительно к маршрутам должны получать маршрут по умолчанию;
3. Маршрутизатор R19 находится в зоне 101 и получает только маршрут по умолчанию;
4. Маршрутизатор R20 находится в зоне 102 и получает все маршруты, кроме маршрутов до сетей зоны 101;
5. Настройка для IPv6 повторяет логику IPv4.

### Решение:

1. Настроим маршрутизаторы R14-R15 в зоне 0 - backbone;
2. Настроим маршрутизаторы R12-R13 в зоне 10. Дополнительно к маршрутам будут получать маршрут по умолчанию;
3. Настроим маршрутизатор R19 в зоне 101 и будет получать только маршрут по умолчанию;
4. Настроим маршрутизатор R20 в зоне 102 и будет получать все маршруты, кроме маршрутов до сетей зоны 101. Задокументируем все изменения.


### 1. Настроим маршрутизаторы R14-R15 в зоне 0 - backbone:

Из-за специфики схемы, в зону backbone попадают в дополнение роутеры R12 и R13.
Исследуемая схема описана [тут.](https://github.com/Pekep97/Labs/tree/main/Lab_04) Для упрощения понимания задублируем в этой работе только нужное:

### Исследуемая схема:

![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_06/OSPF_OTUS.png)


### Таблица адрестного пространства:

|              |            |                 | *Москва*      |                       |             |              |             |                |
|--------------|------------|-----------------|---------------|-----------------------|-------------|--------------|-------------|----------------|
| **Hostname**     | **Interfaces** | **Description**     | **IPv4-address**  | **Mask**                  | **Gateway**     | **IPv6-address** | **IPv6-prefix** | **LLIPv6-address** |
| R12          | e0/0.100   | MANAGEMENT_MSK  | 10.58.100.2   | 255.255.255.0 (/24)   | -           | fd00:10:58:100::1   | /64         | fe80::1        |
|              | e0/1.10    | DHCP_MSK        | 192.168.10.3  | 255.255.255.0 (/24)   | -           | fd00:192:168:10::1  | /64         | fe80::1        |
|              | e0/2       | l3:to-R14       | 10.64.100.1   | 255.255.255.252 (/30) | -           | fd00:0:12:14::1     | /112        | fe80::1        |
|              | e0/3       | l3:to-R15       | 10.64.100.5   | 255.255.255.252 (/30) | -           | fd00:0:12:15::1     | /112        | fe80::1        |
| R13          | e0/0.100   | MANAGEMENT_MSK  | 10.58.100.4   | 255.255.255.0 (/24)   | -           | fd00:10:58:100::1   | /64         | fe80::100      |
|              | e0/1.10    | DHCP_MSK        | 192.168.10.5  | 255.255.255.0 (/24)   | -           | fd00:192:168:10::1  | /64         | fe80::10       |
|              | e0/2       | l3:to-R15       | 10.64.100.13  | 255.255.255.252 (/30) | -           | fd00:0:13:15::1     | /112        | fe80::1        |
|              | e0/3       | l3:to-R14       | 10.64.100.9   | 255.255.255.252 (/30) | -           | fd00:0:13:14::1     | /112        | fe80::1        |
| VRRP_R12+R13 | -          | MANAGEMENT_MSK  | 10.58.100.1   | 255.255.255.0 (/24)   | -           | -                   | -           | -              |
|              | -          | DHCP_MSK        | 192.168.10.1  | 255.255.255.0 (/24)   | -           | -                   | -           | -              |
| R14          | e0/0       | l3:to-R12       | 10.64.100.2   | 255.255.255.252 (/30) | -           | fd00:0:12:14::2     | /112        | fe80::2        |
|              | e0/1       | l3:to-R13       | 10.64.100.13  | 255.255.255.252 (/30) | -           | fd00:0:13:14::2     | /112        | fe80::2        |
|              | e0/2       | l3:to-AS-101    | 85.10.22.2    | 255.255.255.252 (/30) | -           | 2000:0:1001:101::2  | /112        | fe80::2        |
|              | e0/3       | l3:to-R19       | 10.64.100.21  | 255.255.255.252 (/30) | -           | fd00:0:14:19::1     | /112        | fe80::2        |
| R15          | e0/0       | l3:to-R13       | 10.64.100.14  | 255.255.255.252 (/30) | -           | fd00:0:13:15::2     | /112        | fe80::2        |
|              | e0/1       | l3:to-R12       | 10.64.100.6   | 255.255.255.252 (/30) | -           | fd00:0:12:15::2     | /112        | fe80::2        |
|              | e0/2       | l3:to-AS-301    | 132.50.21.2   | 255.255.255.252 (/30) | -           | 2000:0:1001:301::2  | /112        | fe80::2        |
|              | e0/3       | l3:to-R20       | 10.64.100.17  | 255.255.255.252 (/30) | -           | fd00:0:15:20::1     | /112        | fe80::2        |
| R19          | e0/0       | l3:to-R14       | 10.64.100.22  | 255.255.255.252 (/30) | -           | fd00:0:14:19::2     | /112        | fe80::1        |
| R20          | e0/0       | l3:to-R15       | 10.64.100.18  | 255.255.255.252 (/30) | -           | fd00:0:15:20::2     | /112        | fe80::1        |
| SW2          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.12  | 255.255.255.0 (/24)   | 10.58.100.1 | fd00:10:58:100::2   | /64         | fe80::2        |
| SW3          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.13  | 255.255.255.0 (/24)   | 10.58.100.1 | fd00:10:58:100::3   | /64         | fe80::3        |
| SW4          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.14  | 255.255.255.0 (/24)   | 10.58.100.1 | fd00:10:58:100::4   | /64         | fe80::4        |
| SW5          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.15  | 255.255.255.0 (/24)   | 10.58.100.1 | fd00:10:58:100::5   | /64         | fe80::5        |
| VPC1         | NIC        | -               | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |
| VPC2         | NIC        | -               | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |

- Покажем пример настройки на R14:

```
R14#sh run | sec ospf
 ip ospf network point-to-point
 ipv6 ospf 1 area 0
 ipv6 ospf network point-to-point
 ip ospf network point-to-point
 ipv6 ospf 1 area 0
 ipv6 ospf network point-to-point
router ospf 1
 router-id 14.14.14.14
 passive-interface Ethernet0/2
 network 10.64.100.0 0.0.0.3 area 0
 network 10.64.100.8 0.0.0.3 area 0
ipv6 router ospf 1
 router-id 14.14.14.14
 passive-interface Ethernet0/2
```

- Покажем обновленную таблицу маршрутизации:

*IPv4*
```
R14#sh ip route ospf
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

      10.0.0.0/8 is variably subnetted, 8 subnets, 2 masks
O        10.64.100.4/30 [110/20] via 10.64.100.1, 04:03:58, Ethernet0/0
O        10.64.100.8/30 [110/40] via 10.64.100.1, 04:03:48, Ethernet0/0
```

*IPv6*
```
R14#sh ipv6 route ospf
IPv6 Routing Table - default - 11 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, HA - Home Agent, MR - Mobile Router, R - RIP
       H - NHRP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, NM - NEMO
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, la - LISP alt
       lr - LISP site-registrations, ld - LISP dyn-eid, a - Application
O   FD00:0:12:15::/112 [110/20]
     via FE80::1, Ethernet0/0
O   FD00:0:13:15::/112 [110/20]
     via FE80::1, Ethernet0/1
```

### 2. Настроим маршрутизаторы R12-R13 в зоне 10. Дополнительно к маршрутам будут получать маршрут по умолчанию:

- Для выполнения условия, требуется настроить зону 10 как *stub area*, пример покажем на R12:

```
R12#sh run | sec ospf
 ipv6 ospf 1 area 10
 ipv6 ospf 1 area 10
 ip ospf network point-to-point
 ipv6 ospf 1 area 0
 ipv6 ospf network point-to-point
 ip ospf network point-to-point
 ipv6 ospf 1 area 0
 ipv6 ospf network point-to-point
router ospf 1
 router-id 12.12.12.12
 area 10 stub
 network 10.58.100.0 0.0.0.255 area 10
 network 10.64.100.0 0.0.0.3 area 0
 network 10.64.100.4 0.0.0.3 area 0
 network 192.168.10.0 0.0.0.255 area 10
 default-information originate
ipv6 router ospf 1
 router-id 12.12.12.12
 area 10 stub
 default-information originate
```

- Покажем обновленную таблицу маршрутизации на примере R15:

*IPv4*
```
R15#sh ip route
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

      10.0.0.0/8 is variably subnetted, 9 subnets, 3 masks
O IA     10.58.100.0/24 [110/20] via 10.64.100.5, 00:13:22, Ethernet0/1
O        10.64.100.0/30 [110/20] via 10.64.100.5, 00:13:22, Ethernet0/1
C        10.64.100.4/30 is directly connected, Ethernet0/1
L        10.64.100.6/32 is directly connected, Ethernet0/1
O        10.64.100.8/30 [110/20] via 10.64.100.13, 00:13:22, Ethernet0/0
C        10.64.100.12/30 is directly connected, Ethernet0/0
L        10.64.100.14/32 is directly connected, Ethernet0/0
C        10.64.100.16/30 is directly connected, Ethernet0/3
L        10.64.100.17/32 is directly connected, Ethernet0/3
      132.50.0.0/16 is variably subnetted, 2 subnets, 2 masks
C        132.50.21.0/30 is directly connected, Ethernet0/2
L        132.50.21.2/32 is directly connected, Ethernet0/2
O IA  192.168.10.0/24 [110/20] via 10.64.100.13, 00:13:22, Ethernet0/0
                      [110/20] via 10.64.100.5, 00:13:22, Ethernet0/1
```

*IPv6*
```
R15#sh ipv6 route
IPv6 Routing Table - default - 13 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, HA - Home Agent, MR - Mobile Router, R - RIP
       H - NHRP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, NM - NEMO
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, la - LISP alt
       lr - LISP site-registrations, ld - LISP dyn-eid, a - Application
C   2000:0:1001:301::/112 [0/0]
     via Ethernet0/2, directly connected
L   2000:0:1001:301::2/128 [0/0]
     via Ethernet0/2, receive
O   FD00:0:12:14::/112 [110/20]
     via FE80::1, Ethernet0/1
C   FD00:0:12:15::/112 [0/0]
     via Ethernet0/1, directly connected
L   FD00:0:12:15::2/128 [0/0]
     via Ethernet0/1, receive
O   FD00:0:13:14::/112 [110/20]
     via FE80::1, Ethernet0/0
C   FD00:0:13:15::/112 [0/0]
     via Ethernet0/0, directly connected
L   FD00:0:13:15::2/128 [0/0]
     via Ethernet0/0, receive
C   FD00:0:15:20::/112 [0/0]
     via Ethernet0/3, directly connected
L   FD00:0:15:20::1/128 [0/0]
     via Ethernet0/3, receive
OI  FD00:10:58:100::/64 [110/20]
     via FE80::1, Ethernet0/0
     via FE80::1, Ethernet0/1
OI  FD00:192:168:10::/64 [110/20]
     via FE80::1, Ethernet0/0
     via FE80::1, Ethernet0/1
L   FF00::/8 [0/0]
     via Null0, receive
```

- Как видим, добавились сети которые "живут" за R12 и R13 как сети, переданные из другой зоны при помощи LSA-3

### 3. Настроим маршрутизатор R19 в зоне 101 и будет получать только маршрут по умолчанию:

- Для выполнения этого условия настроим зону 101 как *totaly stub area*, для визуализации правильности, представим таблицу маршрутизации роутера R19:

*IPv4*
```
R19#sh ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       a - application route
       + - replicated route, % - next hop override

Gateway of last resort is 10.64.100.21 to network 0.0.0.0

O*IA  0.0.0.0/0 [110/11] via 10.64.100.21, 00:01:00, Ethernet0/0
      10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        10.64.100.20/30 is directly connected, Ethernet0/0
L        10.64.100.22/32 is directly connected, Ethernet0/0
```

*IPv6*
```
R19#sh ipv6 route
IPv6 Routing Table - default - 4 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, HA - Home Agent, MR - Mobile Router, R - RIP
       H - NHRP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, NM - NEMO
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, la - LISP alt
       lr - LISP site-registrations, ld - LISP dyn-eid, a - Application
OI  ::/0 [110/11]
     via FE80::2, Ethernet0/0
C   FD00:0:14:19::/112 [0/0]
     via Ethernet0/0, directly connected
L   FD00:0:14:19::2/128 [0/0]
     via Ethernet0/0, receive
L   FF00::/8 [0/0]
     via Null0, receive
```

- Исходя из таблицы маршрутизации видно, что доступ к любой сети за пределами R19 будет направляться на интерфейс e0/3 роутера R14.
- Удостоверимся в работе маршрутизации при помощи утилиты *ping*, проверим доступность IPv4 - адреса 10.64.100.1 (пренадлежит интерфейсу роутера R12)

```
R19#ping 10.64.100.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.64.100.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
```

### 4. Настроим маршрутизатор R20 в зоне 102 и будет получать все маршруты, кроме маршрутов до сетей зоны 101. Задокументируем все изменения:

- Для реализации этого задания, потребуется настроить зону 102 как *standart area* и создать *prefix-list* area_101_deny на роутере R15.
- Покажем результаты настройки на роутере R15, R20 и его таблицу маршрутизации:

*prefix-list*
```
R15#sh run | section prefix
 area 102 filter-list prefix area_101_deny in
ip prefix-list area_101_deny seq 5 deny 10.64.100.20/30
ip prefix-list area_101_deny seq 10 permit 0.0.0.0/0 le 32
 area 102 filter-list prefix area_101_deny in
ipv6 prefix-list area_101_deny seq 5 deny FD00:0:14:19::/112
ipv6 prefix-list area_101_deny seq 10 permit ::/0 le 128
```

*IPv4*
```
R20#sh ip route
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

      10.0.0.0/8 is variably subnetted, 7 subnets, 3 masks
O IA     10.58.100.0/24 [110/30] via 10.64.100.17, 00:21:47, Ethernet0/0
O IA     10.64.100.0/30 [110/30] via 10.64.100.17, 00:21:47, Ethernet0/0
O IA     10.64.100.4/30 [110/20] via 10.64.100.17, 00:21:47, Ethernet0/0
O IA     10.64.100.8/30 [110/30] via 10.64.100.17, 00:21:47, Ethernet0/0
O IA     10.64.100.12/30 [110/20] via 10.64.100.17, 00:21:47, Ethernet0/0
C        10.64.100.16/30 is directly connected, Ethernet0/0
L        10.64.100.18/32 is directly connected, Ethernet0/0
O IA  192.168.10.0/24 [110/30] via 10.64.100.17, 00:21:47, Ethernet0/0
```

*IPv6*
```
R20#sh ipv6 route
IPv6 Routing Table - default - 9 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, HA - Home Agent, MR - Mobile Router, R - RIP
       H - NHRP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, NM - NEMO
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, la - LISP alt
       lr - LISP site-registrations, ld - LISP dyn-eid, a - Application
OI  FD00:0:12:14::/112 [110/30]
     via FE80::2, Ethernet0/0
OI  FD00:0:12:15::/112 [110/20]
     via FE80::2, Ethernet0/0
OI  FD00:0:13:14::/112 [110/30]
     via FE80::2, Ethernet0/0
OI  FD00:0:13:15::/112 [110/20]
     via FE80::2, Ethernet0/0
C   FD00:0:15:20::/112 [0/0]
     via Ethernet0/0, directly connected
L   FD00:0:15:20::2/128 [0/0]
     via Ethernet0/0, receive
OI  FD00:10:58:100::/64 [110/30]
     via FE80::2, Ethernet0/0
OI  FD00:192:168:10::/64 [110/30]
     via FE80::2, Ethernet0/0
L   FF00::/8 [0/0]
     via Null0, receive
```
  
- Как видно из таблицы маршрутизации, в нее не попали сети, указанные в задании, а именно:
 - 10.64.100.20/30;
 - FD00:0:14:19::/112

- Все изменения приведены [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_06/Configs) 
