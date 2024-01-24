# iBGP

### Задание:

1. Настройте iBGP в офисе Москва между маршрутизаторами R14 и R15;
2. Настройте iBGP в провайдере Триада, с использованием RR;
3. Настройте офиса Москва так, чтобы приоритетным провайдером стал Ламас;
4. Настройте офиса С.-Петербург так, чтобы трафик до любого офиса распределялся по двум линкам одновременно;
5. Все сети в лабораторной работе должны иметь IP связность.

### Решение:

1. Настроим iBGP в офисе Москва между маршрутизаторами R14 и R15;
2. Настроим iBGP в провайдере Триада, с использованием RR;
3. Настроим офис Москва так, чтобы приоритетным провайдером стал Ламас;
4. Настроим офис С.-Петербург так, чтобы трафик до любого офиса распределялся по двум линкам одновременно;
5. Проверим все сети в лабораторной работе на IP связность и задокументируем все изменения.

### 1. Настроим iBGP в офисе Москва между маршрутизаторами R14 и R15:

- Исследуемая схема описана [тут.](https://github.com/Pekep97/Labs/tree/main/Lab_04) Для упрощения понимания задублируем в этой работе только нужное:

### Исследуемая схема:

![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_04/Lab_04.png)

### Таблица адресного пространства:

|              |            |                 | *Москва*        |                       |             |                     |             |                |
|--------------|------------|-----------------|---------------|-----------------------|-------------|---------------------|-------------|----------------|
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address        | IPv6-prefix | LLIPv6-address |
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
|              | Loopback0  | -               | 14.14.14.14   | 255.255.255.255(/32)  | -           | fd00:14:14:14::14   | /128        | fe80::1        |
| R15          | e0/0       | l3:to-R13       | 10.64.100.14  | 255.255.255.252 (/30) | -           | fd00:0:13:15::2     | /112        | fe80::2        |
|              | e0/1       | l3:to-R12       | 10.64.100.6   | 255.255.255.252 (/30) | -           | fd00:0:12:15::2     | /112        | fe80::2        |
|              | e0/2       | l3:to-AS-301    | 132.50.21.2   | 255.255.255.252 (/30) | -           | 2000:0:1001:301::2  | /112        | fe80::2        |
|              | e0/3       | l3:to-R20       | 10.64.100.17  | 255.255.255.252 (/30) | -           | fd00:0:15:20::1     | /112        | fe80::2        |
|              | Loopback0  | -               | 15.15.15.15   | 255.255.255.255(/32)  | -           | fd00:15:15:15::15   | /128        | fe80::1        |
| R19          | e0/0       | l3:to-R14       | 10.64.100.22  | 255.255.255.252 (/30) | -           | fd00:0:14:19::2     | /112        | fe80::1        |
| R20          | e0/0       | l3:to-R15       | 10.64.100.18  | 255.255.255.252 (/30) | -           | fd00:0:15:20::2     | /112        | fe80::1        |
| SW2          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.12  | 255.255.255.0 (/24)   | 10.58.100.1 | fd00:10:58:100::2   | /64         | fe80::2        |
| SW3          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.13  | 255.255.255.0 (/24)   | 10.58.100.1 | fd00:10:58:100::3   | /64         | fe80::3        |
| SW4          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.14  | 255.255.255.0 (/24)   | 10.58.100.1 | fd00:10:58:100::4   | /64         | fe80::4        |
| SW5          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.15  | 255.255.255.0 (/24)   | 10.58.100.1 | fd00:10:58:100::5   | /64         | fe80::5        |
| VPC1         | NIC        | -               | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |
| VPC2         | NIC        | -               | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |
|              |            |                 | *Киторн*        |                       |             |                     |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address        | IPv6-prefix | LLIPv6-address |
| R22          | e0/0       | l3:to-AS-1001   | 85.10.22.1    | 255.255.255.252 (/30) | -           | 2000:0:1001:101::1  | /112        | fe80::1        |
|              | e0/1       | l3:to-AS-301    | 21.22.100.1   | 255.255.255.252 (/30) | -           | 2000:0:301:101::1   | /112        | fe80::2        |
|              | e0/2       | l3:to-AS-520    | 23.100.40.2   | 255.255.255.252 (/30) | -           | 2000:0:520:101::2   | /112        | fe80::1        |
|              |            |                 | *Ламас*         |                       |             |                     |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address        | IPv6-prefix | LLIPv6-address |
| R21          | e0/0       | l3:to-AS-1001   | 132.50.21.1   | 255.255.255.252 (/30) | -           | 2000:0:1001:301::1  | /112        | fe80::1        |
|              | e0/1       | l3:to-AS-101    | 21.22.100.2   | 255.255.255.252 (/30) | -           | 2000:0:301:101::2   | /112        | fe80::1        |
|              | e0/2       | l3:to-AS-520    | 24.100.40.2   | 255.255.255.252 (/30) | -           | 2000:0:520:301::2   | /112        | fe80::1        |
|              |            |                 | *Триада*        |                       |             |                     |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address        | IPv6-prefix | LLIPv6-address |
| R23          | e0/0       | l3:to-AS-101    | 23.100.40.1   | 255.255.255.252 (/30) | -           | 2000:0:520:101::1   | /112        | fe80::2        |
|              | e0/1       | l3:to-R25       | 10.64.52.1    | 255.255.255.252 (/30) | -           | fd00:0:23:25::1     | /112        | fe80::1        |
|              | e0/2       | l3:to-R24       | 10.64.52.5    | 255.255.255.252 (/30) | -           | fd00:0:23:24::1     | /112        | fe80::1        |
|              | Loopback0  | -               | 23.23.23.23   | 255.255.255.255(/32)  | -           | fd00:23:23:23::23   | /128        | fe80::1        |
| R24          | e0/0       | l3:to-AS-301    | 24.100.40.1   | 255.255.255.252 (/30) | -           | 2000:0:520:301::1   | /112        | fe80::2        |
|              | e0/1       | l3:to-R26       | 10.64.52.9    | 255.255.255.252 (/30) | -           | fd00:0:24:26::1     | /112        | fe80::2        |
|              | e0/2       | l3:to-R23       | 10.64.52.6    | 255.255.255.252 (/30) | -           | fd00:0:23:24::2     | /112        | fe80::2        |
|              | e0/3       | l3:to-AS-2042   | 24.100.40.5   | 255.255.255.252 (/30) | -           | 2000:0:520:2042::1  | /112        | fe80::2        |
|              | Loopback0  | -               | 24.24.24.24   | 255.255.255.255(/32)  | -           | fd00:24:24:24::24   | /128        | fe80::1        |
| R25          | e0/0       | l3:to-R23       | 10.64.52.2    | 255.255.255.252 (/30) | -           | fd00:0:23:25::2     | /112        | fe80::2        |
|              | e0/1       | l3:to-LBTNG     | 1.1.1.2       | 255.255.255.252 (/30) | -           | 2000:0:520:1111::2  | /112        | fe80::2        |
|              | e0/2       | l3:to-R26       | 10.64.52.13   | 255.255.255.252 (/30) | -           | fd00:0:25:26::1     | /112        | fe80::2        |
|              | e0/3       | l3:to-CHKR      | 2.2.2.2       | 255.255.255.252 (/30) | -           | 2000:0:520:2222::2  | /112        | fe80::2        |
|              | Loopback0  | -               | 25.25.25.25   | 255.255.255.255(/32)  | -           | fd00:25:25:25::25   | /128        | fe80::1        |
| R26          | e0/0       | l3:to-R24       | 10.64.52.10   | 255.255.255.252 (/30) | -           | fd00:0:24:26::2     | /112        | fe80::1        |
|              | e0/1       | l3:to-CHKR      | 3.3.3.2       | 255.255.255.252 (/30) | -           | 2000:0:520:3333::2  | /112        | fe80::1        |
|              | e0/2       | l3:to-R25       | 10.64.52.14   | 255.255.255.252 (/30) | -           | fd00:0:25:26::2     | /112        | fe80::1        |
|              | e0/3       | l3:to-AS-2042   | 26.100.40.1   | 255.255.255.252 (/30) | -           | 2000:0:2042:520::1  | /112        | fe80::1        |
|              | Loopback0  | -               | 26.26.26.26   | 255.255.255.255(/32)  | -           | fd00:26:26:26::26   | /128        | fe80::1        |
|              |            |                 | *Лабытнанги*    |                       |             |                     |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address        | IPv6-prefix | LLIPv6-address |
| R27          | e0/0       | l3:to-AS-520    | 1.1.1.1       | 255.255.255.252 (/30) | -           | 2000:0:520:1111::1  | /112        | fe80::1        |
|              |            |                 | *С.-Петербург*  |                       |             |                     |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address        | IPv6-prefix | LLIPv6-address |
| R16          | e0/0.200   | MANAGEMENT_SPB  | 10.58.200.2   | 255.255.255.0 (/24)   | -           | fd00:10:58:200::1   | /64         | fe80::1        |
|              | e0/2.20    | DHCP_SPB        | 192.168.20.2  | 255.255.255.0 (/24)   | -           | fd00:192:168:20::1  | /64         | fe80::1        |
|              | e0/1       | l3:to-R18       | 10.64.20.6    | 255.255.255.252 (/30) | -           | fd00:0:16:18::2     | /112        | fe80::2        |
|              | e0/3       | l3:to-R32       | 10.64.20.9    | 255.255.255.252 (/30) | -           | fd00:0:16:32::1     | /112        | fe80::1        |
| R17          | e0/0.200   | MANAGEMENT_SPB  | 10.58.200.3   | 255.255.255.0 (/24)   | -           | fd00:10:58:200::1   | /64         | fe80::1        |
|              | e0/2.20    | DHCP_SPB        | 192.168.20.3  | 255.255.255.0 (/24)   | -           | fd00:192:168:200::1 | /64         | fe80::1        |
|              | e0/1       | l3:to-R18       | 10.64.20.2    | 255.255.255.252 (/30) | -           | fd00:0:17:18::2     | /112        | fe80::2        |
| R18          | e0/0       | l3:to-R16       | 10.64.20.5    | 255.255.255.252 (/30) | -           | fd00:0:16:18::1     | /112        | fe80::1        |
|              | e0/1       | l3:to-R17       | 10.64.20.1    | 255.255.255.252 (/30) | -           | fd00:0:17:18::1     | /112        | fe80::1        |
|              | e0/2       | l3:to-AS-520    | 24.100.40.6   | 255.255.255.252 (/30) | -           | 2000:0:520:2042::2  | /112        | fe80::1        |
|              | e0/3       | l3:to-AS-520    | 26.100.40.2   | 255.255.255.252 (/30) | -           | 2000:0:2042:520::2  | /112        | fe80::2        |
| R32          | e0/0       | l3:to-R16       | 10.64.20.10   | 255.255.255.252 (/30) | -           | fd00:0:16:32::2     | /112        | fe80::2        |
| VRRP_R16+R17 | -          | MANAGEMENT_SPB  | 10.58.200.1   | 255.255.255.0 (/24)   | -           | -                   | -           | -              |
|              | -          | DHCP_SPB        | 192.168.20.1  | 255.255.255.0 (/24)   | -           | -                   | -           | -              |
| SW9          | VLAN200    | MANAGEMENT_SPB  | 10.58.200.109 | 255.255.255.0 (/24)   | 10.58.200.1 | fd00:10:58:200::9   | /64         | fe80::9        |
| SW10         | VLAN200    | MANAGEMENT_SPB  | 10.58.200.110 | 255.255.255.0 (/24)   | 10.58.200.1 | fd00:10:58:200::10  | /64         | fe80::10       |
| VPC          | NIC        | -               | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |
| VPC8         | NIC        | -               | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |
|              |            |                 | *Чокурдах*      |                       |             |                     |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address        | IPv6-prefix | LLIPv6-address |
| R28          | e0/2.100   | MANAGEMENT_CHKR | 10.58.10.1    | 255.255.255.0 (/24)   | -           | fd00:10:58:10::1    | /64         | fe80::1        |
|              | e0/2.10    | DHCP_CHKR       | 192.168.100.1 | 255.255.255.0 (/24)   | -           | fd00:192:168:100::1 | /64         | fe80::1        |
|              | e0/0       | l3:to-AS-520    | 3.3.3.1       | 255.255.255.252 (/30) | -           | 2000:0:520:3333::1  | /112        | fe80::2        |
|              | e0/1       | l3:to-AS-520    | 2.2.2.1       | 255.255.255.252 (/30) | -           | 2000:0:520:2222::1  | /112        | fe80::1        |
| SW29         | VLAN100    | MANAGEMENT_CHKR | 10.58.10.129  | 255.255.255.0 (/24)   | 10.58.10.1  | fd00:10:58:10::29   | /64         | fe80::29       |
| VPC30        | -          | -               | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |
| VPC31        | -          | -               | DHCP          | DHCP                  | DHCP        | -                   | -           | -              |

### Таблица VLAN

| Офис         | VLAN-№ | VLAN-NAME       |
| ------------ | ------ | --------------- |
| Москва       | 10     | DHCP_MSK        |
|              | 100    | MANAGEMENT_MSK  |
| С.-Петербург | 20     | DHCP_SPB        |
|              | 200    | MANAGEMENT_SPB  |
| Чокурдах     | 10     | DHCP_CHKR       |
|              | 100    | MANAGEMENT_CHKR |

- Для организации сессий iBGP на маршрутизаторах создадим интерфейсы ***Loopback0*** и назначим IP-адреса согласно [таблице](https://github.com/Pekep97/Labs/tree/main/Lab_10#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%BD%D0%BE%D0%B3%D0%BE-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%B0) для реализации отказоустойчивости, добавим назначенные сети в IGP протоколы офиса Москва. 
- Настроим iBGP в офисе Москва между маршрутизаторами R14 и R15, покажем настройку на R14:

***R14***
```
R14#sh run | sec bgp
router bgp 1001
 bgp router-id 14.14.14.14
 bgp log-neighbor-changes
 neighbor 15.15.15.15 remote-as 1001
 neighbor 15.15.15.15 update-source Loopback0
 neighbor 2000:0:1001:101::1 remote-as 101
 neighbor 85.10.22.1 remote-as 101
 neighbor FD00:15:15:15::15 remote-as 1001
 neighbor FD00:15:15:15::15 update-source Loopback0
 !
 address-family ipv4
  neighbor 15.15.15.15 activate
  no neighbor 2000:0:1001:101::1 activate
  neighbor 85.10.22.1 activate
  neighbor 85.10.22.1 next-hop-self
  no neighbor FD00:15:15:15::15 activate
 exit-address-family
 !
 address-family ipv6
  neighbor 2000:0:1001:101::1 activate
  neighbor 2000:0:1001:101::1 next-hop-self
  neighbor FD00:15:15:15::15 activate
 exit-address-family
```

- Покажем часть вывода команды ***sh ip bgp neighbors 15.15.15.15*** на маршрутизаторе R14:

***R14***
```
R14#sh ip bgp neighbors 15.15.15.15
BGP neighbor is 15.15.15.15,  remote AS 1001, internal link
  BGP version 4, remote router ID 15.15.15.15
  BGP state = Established, up for 2d21h
  Last read 00:00:19, last write 00:00:16, hold time is 180, keepalive interval is 60 seconds
  Neighbor sessions:
    1 active, is not multisession capable (disabled)
  Neighbor capabilities:
    Route refresh: advertised and received(new)
    Four-octets ASN Capability: advertised and received
    Address family IPv4 Unicast: advertised and received
    Enhanced Refresh Capability: advertised and received
    Multisession Capability:
    Stateful switchover support enabled: NO for session 1
  Message statistics:
    InQ depth is 0
    OutQ depth is 0

                         Sent       Rcvd
    Opens:                  1          1
    Notifications:          0          0
    Updates:               18         14
    Keepalives:          4564       4571
    Route Refresh:          0          0
    Total:               4583       4586
  Default minimum time between advertisement runs is 0 second
```

### 2. Настройте iBGP в провайдере Триада, с использованием RR:

- Для организации сессий iBGP на маршрутизаторах создадим интерфейсы ***Loopback0*** и назначим IP-адреса согласно [таблице](https://github.com/Pekep97/Labs/tree/main/Lab_10#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%BD%D0%BE%D0%B3%D0%BE-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%B0) для реализации отказоустойчивости, добавим назначенные сети в IGP протоколы офиса Триада.
- Пусть RR будет маршрутизатор R23, так как он имеет наименьший ***BGP-router ID***. Покажем его конфигурацию, так как настройка остальных маршрутизаторов не покажет наличие в сети RR:

***R23***
```
R23#sh run | sec bgp
router bgp 520
 bgp router-id 23.23.23.23
 bgp cluster-id 23.23.23.23
 bgp log-neighbor-changes
 neighbor 23.100.40.2 remote-as 101
 neighbor 24.24.24.24 remote-as 520
 neighbor 24.24.24.24 update-source Loopback0
 neighbor 25.25.25.25 remote-as 520
 neighbor 25.25.25.25 update-source Loopback0
 neighbor 26.26.26.26 remote-as 520
 neighbor 26.26.26.26 update-source Loopback0
 neighbor 2000:0:520:101::2 remote-as 101
 neighbor FD00:24:24:24::24 remote-as 520
 neighbor FD00:24:24:24::24 update-source Loopback0
 neighbor FD00:25:25:25::25 remote-as 520
 neighbor FD00:25:25:25::25 update-source Loopback0
 neighbor FD00:26:26:26::26 remote-as 520
 neighbor FD00:26:26:26::26 update-source Loopback0
 !
 address-family ipv4
  neighbor 23.100.40.2 activate
  neighbor 23.100.40.2 next-hop-self
  neighbor 24.24.24.24 activate
  neighbor 24.24.24.24 route-reflector-client
  neighbor 25.25.25.25 activate
  neighbor 25.25.25.25 route-reflector-client
  neighbor 26.26.26.26 activate
  neighbor 26.26.26.26 route-reflector-client
  no neighbor 2000:0:520:101::2 activate
  no neighbor FD00:24:24:24::24 activate
  no neighbor FD00:25:25:25::25 activate
  no neighbor FD00:26:26:26::26 activate
 exit-address-family
 !
 address-family ipv6
  neighbor 2000:0:520:101::2 activate
  neighbor 2000:0:520:101::2 next-hop-self
  neighbor FD00:24:24:24::24 activate
  neighbor FD00:24:24:24::24 route-reflector-client
  neighbor FD00:25:25:25::25 activate
  neighbor FD00:25:25:25::25 route-reflector-client
  neighbor FD00:26:26:26::26 activate
  neighbor FD00:26:26:26::26 route-reflector-client
 exit-address-family
```

- Покажем результат выполнения команды ***sh ip bgp summary*** на маршрутизаторе R23:

***R23***
```
R23#sh ip bgp summary
BGP router identifier 23.23.23.23, local AS number 520
BGP table version is 14, main routing table version 14
13 network entries using 1820 bytes of memory
13 path entries using 1040 bytes of memory
4/4 BGP path/bestpath attribute entries using 576 bytes of memory
3 BGP AS-PATH entries using 72 bytes of memory
0 BGP route-map cache entries using 0 bytes of memory
0 BGP filter-list cache entries using 0 bytes of memory
BGP using 3508 total bytes of memory
BGP activity 26/0 prefixes, 26/0 paths, scan interval 60 secs

Neighbor        V           AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
23.100.40.2     4          101       0       0        1    0    0 never    Idle
24.24.24.24     4          520    1716    1713       14    0    0 1d01h          13
25.25.25.25     4          520     191     195       14    0    0 02:50:29        0
26.26.26.26     4          520     166     172       14    0    0 02:27:54        0
```

### 3. Настроим офис Москва так, чтобы приоритетным провайдером стал Ламас:

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

### 4. Настроим офис С.-Петербург так, чтобы трафик до любого офиса распределялся по двум линкам одновременно:

- Для выполнения этого условия требуется на маршрутизаторе R18 прописать команду *maximum-paths 2* которая автоматически распределяет между несколькими линками трафик (в нашем случае - 2), направленный в одну сеть. Покажем конфигурацию R18:

***R18***
```
R18#sh run | sec bgp
router bgp 2042
 bgp router-id 18.18.18.18
 bgp log-neighbor-changes
 neighbor 24.100.40.5 remote-as 520
 neighbor 26.100.40.1 remote-as 520
 neighbor 2000:0:520:2042::1 remote-as 520
 !
 address-family ipv4
  redistribute eigrp 1
  neighbor 24.100.40.5 activate
  neighbor 24.100.40.5 next-hop-self
  neighbor 26.100.40.1 activate
  neighbor 26.100.40.1 next-hop-self
  no neighbor 2000:0:520:2042::1 activate
  maximum-paths 2
 exit-address-family
 !
 address-family ipv6
  maximum-paths 2
  neighbor 2000:0:520:2042::1 activate
  neighbor 2000:0:520:2042::1 next-hop-self
 exit-address-family
```

- В результате выполнения команды *sh ip bgp* видно, что все сети будут распределяться по двум сессиям:

***R18***
```
R18#sh ip bgp
BGP table version is 29, local router ID is 18.18.18.18
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *m  1.1.1.0/30       26.100.40.1                            0 520 i
 *>                   24.100.40.5                            0 520 i
 *m  2.2.2.0/30       26.100.40.1                            0 520 i
 *>                   24.100.40.5                            0 520 i
 *m  3.3.3.0/30       26.100.40.1              0             0 520 i
 *>                   24.100.40.5                            0 520 i
 *m  10.58.100.0/24   26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *>  10.58.200.0/24   10.64.20.2         1536000         32768 ?
 *>  10.64.20.0/30    0.0.0.0                  0         32768 ?
 *>  10.64.20.8/30    10.64.20.2         2048000         32768 ?
 *m  10.64.52.0/30    26.100.40.1                            0 520 i
 *>                   24.100.40.5                            0 520 i
 *m  10.64.52.4/30    26.100.40.1                            0 520 i
     Network          Next Hop            Metric LocPrf Weight Path
 *>                   24.100.40.5              0             0 520 i
 *m  10.64.52.8/30    26.100.40.1              0             0 520 i
 *>                   24.100.40.5              0             0 520 i
 *m  10.64.52.12/30   26.100.40.1              0             0 520 i
 *>                   24.100.40.5                            0 520 i
 *m  10.64.100.0/30   26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *m  10.64.100.4/30   26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *m  10.64.100.8/30   26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *m  10.64.100.12/30  26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *m  10.64.100.16/30  26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *m  10.64.100.20/30  26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *m  14.14.14.14/32   26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *m  15.15.15.15/32   26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *   21.22.100.0/30   26.100.40.1                            0 520 101 i
     Network          Next Hop            Metric LocPrf Weight Path
 *>                   24.100.40.5                            0 520 301 i
 *m  23.100.40.0/30   26.100.40.1                            0 520 i
 *>                   24.100.40.5                            0 520 i
 *m  24.100.40.0/30   26.100.40.1                            0 520 i
 *>                   24.100.40.5              0             0 520 i
 rm  24.100.40.4/30   26.100.40.1                            0 520 i
 r>                   24.100.40.5              0             0 520 i
 rm  26.100.40.0/30   26.100.40.1              0             0 520 i
 r>                   24.100.40.5                            0 520 i
 *m  85.10.22.0/30    26.100.40.1                            0 520 101 i
 *>                   24.100.40.5                            0 520 101 i
 *m  132.50.21.0/30   26.100.40.1                            0 520 301 i
 *>                   24.100.40.5                            0 520 301 i
 *m  192.168.10.0     26.100.40.1                            0 520 301 1001 ?
 *>                   24.100.40.5                            0 520 301 1001 ?
 *>  192.168.20.0     10.64.20.2         1536000         32768 ?
```

  ### 5. Проверим все сети в лабораторной работе на IP связность и задокументируем все изменения:

  
