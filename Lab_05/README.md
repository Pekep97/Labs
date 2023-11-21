# PBR

### Задание:

1. Настроить политику маршрутизации в офисе Чокурдах;
2. Распределить трафик между 2 линками;

### Решение:

1. [Настроим политику маршрутизации для сетей офиса;](https://github.com/Pekep97/Labs/blob/main/Lab_05/README.md#1-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BF%D0%BE%D0%BB%D0%B8%D1%82%D0%B8%D0%BA%D1%83-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8-%D0%B4%D0%BB%D1%8F-%D1%81%D0%B5%D1%82%D0%B5%D0%B9-%D0%BE%D1%84%D0%B8%D1%81%D0%B0)
2. [Распределим трафик между двумя линками с провайдером;](https://github.com/Pekep97/Labs/blob/main/Lab_05/README.md#2-%D1%80%D0%B0%D1%81%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D0%B8%D0%BC-%D1%82%D1%80%D0%B0%D1%84%D0%B8%D0%BA-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-%D0%B4%D0%B2%D1%83%D0%BC%D1%8F-%D0%BB%D0%B8%D0%BD%D0%BA%D0%B0%D0%BC%D0%B8-%D1%81-%D0%BF%D1%80%D0%BE%D0%B2%D0%B0%D0%B9%D0%B4%D0%B5%D1%80%D0%BE%D0%BC)
3. [Настроим отслеживание линка через технологию IP SLA.(только для IPv4);](https://github.com/Pekep97/Labs/blob/main/Lab_05/README.md#3-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BE%D1%82%D1%81%D0%BB%D0%B5%D0%B6%D0%B8%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BB%D0%B8%D0%BD%D0%BA%D0%B0-%D1%87%D0%B5%D1%80%D0%B5%D0%B7-%D1%82%D0%B5%D1%85%D0%BD%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8E-ip-sla%D1%82%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE-%D0%B4%D0%BB%D1%8F-ipv4)
4. [Настроим для офиса Лабытнанги маршрут по-умолчанию и задокументируем все изменения.](https://github.com/Pekep97/Labs/blob/main/Lab_05/README.md#4-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%B4%D0%BB%D1%8F-%D0%BE%D1%84%D0%B8%D1%81%D0%B0-%D0%BB%D0%B0%D0%B1%D1%8B%D1%82%D0%BD%D0%B0%D0%BD%D0%B3%D0%B8-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82-%D0%BF%D0%BE-%D1%83%D0%BC%D0%BE%D0%BB%D1%87%D0%B0%D0%BD%D0%B8%D1%8E-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)

### 1. Настроим политику маршрутизации для сетей офиса:

Настройки дополняют схему, которая отображена [тут.](https://github.com/Pekep97/Labs/edit/main/Lab_04)
Для наглядности, основные параметры задублируем.

### Исследуемая схема

![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_04/Lab_04.png)

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
|              |            |                 | *Киторн*      |                       |             |              |             |                |
| **Hostname**     | **Interfaces** | **Description**     | **IPv4-address**  | **Mask**                  | **Gateway**     | **IPv6-address** | **IPv6-prefix** | **LLIPv6-address** |
| R22          | e0/0       | l3:to-AS-1001   | 85.10.22.1    | 255.255.255.252 (/30) | -           | 2000:0:1001:101::1  | /112        | fe80::1        |
|              | e0/1       | l3:to-AS-301    | 21.22.100.1   | 255.255.255.252 (/30) | -           | 2000:0:301:101::1   | /112        | fe80::2        |
|              | e0/2       | l3:to-AS-520    | 23.100.40.2   | 255.255.255.252 (/30) | -           | 2000:0:520:101::2   | /112        | fe80::1        |
|              |            |                 | *Ламас*       |                       |             |              |             |                |
| **Hostname**     | **Interfaces** | **Description**     | **IPv4-address**  | **Mask**                  | **Gateway**     | **IPv6-address** | **IPv6-prefix** | **LLIPv6-address** |
| R21          | e0/0       | l3:to-AS-1001   | 132.50.21.1   | 255.255.255.252 (/30) | -           | 2000:0:1001:301::1  | /112        | fe80::1        |
|              | e0/1       | l3:to-AS-101    | 21.22.100.2   | 255.255.255.252 (/30) | -           | 2000:0:301:101::2   | /112        | fe80::1        |
|              | e0/2       | l3:to-AS-520    | 24.100.40.2   | 255.255.255.252 (/30) | -           | 2000:0:520:301::2   | /112        | fe80::1        |
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
|              |            |                 | *Лабытнанги*  |                       |             |              |             |                |
| **Hostname**     | **Interfaces** | **Description**     | **IPv4-address**  | **Mask**                  | **Gateway**     | **IPv6-address** | **IPv6-prefix** | **LLIPv6-address** |
| R27          | e0/0       | l3:to-AS-520    | 1.1.1.1       | 255.255.255.252 (/30) | -           | 2000:0:520:1111::1  | /112        | fe80::1        |
|              |            |                 | *С.-Петербург*|                       |             |              |             |                |
| **Hostname**     | **Interfaces** | **Description**     | **IPv4-address**  | **Mask**                  | **Gateway**     | **IPv6-address** | **IPv6-prefix** | **LLIPv6-address** |
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
|              |            |                 | *Чокурдах*    |                       |             |              |             |                |
| **Hostname**     | **Interfaces** | **Description**     | **IPv4-address**  | **Mask**                  | **Gateway**     | **IPv6-address** | **IPv6-prefix** | **LLIPv6-address** |
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

- Настроим статическую маршрутизацию с роутеров R25, R26 к сетям 192.168.100.0/24 и 10.58.10.0/24; для примера покажем связность при помощи утилиты *ping* с VPC на интерфейсы роутеров R25, R26:

```
VPCS> ping 2.2.2.2

84 bytes from 2.2.2.2 icmp_seq=1 ttl=254 time=0.619 ms
84 bytes from 2.2.2.2 icmp_seq=2 ttl=254 time=0.786 ms
84 bytes from 2.2.2.2 icmp_seq=3 ttl=254 time=0.759 ms
84 bytes from 2.2.2.2 icmp_seq=4 ttl=254 time=0.764 ms
84 bytes from 2.2.2.2 icmp_seq=5 ttl=254 time=0.705 ms

VPCS> ping 3.3.3.2

84 bytes from 3.3.3.2 icmp_seq=1 ttl=254 time=0.795 ms
84 bytes from 3.3.3.2 icmp_seq=2 ttl=254 time=0.770 ms
84 bytes from 3.3.3.2 icmp_seq=3 ttl=254 time=0.753 ms
84 bytes from 3.3.3.2 icmp_seq=4 ttl=254 time=0.832 ms
84 bytes from 3.3.3.2 icmp_seq=5 ttl=254 time=0.768 ms
```
Как видно из проверки, все что нужно - доступно.

- создадим *access-lists* и *route-maps* на роутере R28 и привяжем их к интерфейсам для распределения трафика по интерфейсам (трафик из сети 192.168.100.0/24 будет ходить через 2.2.2.2, а 10.58.10.0/24 - через 3.3.3.2), смотрящим в сторону R25 и R26 соответственно:

***acess-lists***
```
R28#sh access-lists
Extended IP access list 100 // разрешает трафик из сети 192.168.100.0/24 к любому адреса назначения
    10 permit ip 192.168.100.0 0.0.0.255 any
Extended IP access list 101 // разрешает трафик из сети 10.58.10.0/24 к любому адреса назначения
    10 permit ip 10.58.10.0 0.0.0.255 any (20 matches)
IPv6 access list permit_to-R25 // разрешает трафик из сети FD00:192:168:100::/64 к любому адреса назначения
    permit ipv6 FD00:192:168:100::/64 any sequence 10
IPv6 access list permit_to-R26 // разрешает трафик из сети FD00:10:58:10::/64 к любому адреса назначения
    permit ipv6 FD00:10:58:10::/64 any sequence 10
```

***route-maps***
```
R28#sh route-map
route-map permit_to-R26, permit, sequence 10 // перенаправляет весь трафик, указанный в *acess-list* на интерфейс e0/0 роутера R28
  Match clauses:
    ip address (access-lists): 101
     ipv6 address permit_to-R26
  Set clauses:
    ip next-hop 3.3.3.2
     ipv6 next-hop 2000:0:520:3333::2
  Policy routing matches: 20 packets, 2360 bytes
route-map permit_to-R25, permit, sequence 10 // перенаправляет весь трафик, указанный в *acess-list* на интерфейс e0/1 роутера R28
  Match clauses:
    ip address (access-lists): 100
     ipv6 address permit_to-R25
  Set clauses:
    ip next-hop 2.2.2.2
     ipv6 next-hop 2000:0:520:2222::2
  Policy routing matches: 0 packets, 0 bytes
```

### 2. Распределим трафик между двумя линками с провайдером:

- для распределения трафика, применим выше указанные политики на интерфейсы роутера R28:

```
R28#sh run interface e0/2.10
Building configuration...

Current configuration : 237 bytes
!
interface Ethernet0/2.10
 description DHCP_CHKR
 encapsulation dot1Q 10
 ip address 192.168.100.1 255.255.255.0
 ip policy route-map permit_to-R25
 ipv6 address FE80::1 link-local
 ipv6 address FD00:192:168:100::1/64
 ipv6 enable
end

R28#sh run interface e0/2.100
Building configuration...

Current configuration : 239 bytes
!
interface Ethernet0/2.100
 description MANAGEMENT_CHKR
 encapsulation dot1Q 100
 ip address 10.58.10.1 255.255.255.0
 ip policy route-map permit_to-R26
 ipv6 address FE80::1 link-local
 ipv6 address FD00:10:58:10::1/64
 ipv6 enable
end
```

После проделанных манипуляций, повторно запустим *ping* с VPC и SW29 (с VPC должен быть ping только на 2.2.2.2, с SW29 - успешным на 3.3.3.2):

VPC
```
VPCS> ping 2.2.2.2

84 bytes from 2.2.2.2 icmp_seq=1 ttl=254 time=0.582 ms
84 bytes from 2.2.2.2 icmp_seq=2 ttl=254 time=0.700 ms
84 bytes from 2.2.2.2 icmp_seq=3 ttl=254 time=0.911 ms
84 bytes from 2.2.2.2 icmp_seq=4 ttl=254 time=0.848 ms
84 bytes from 2.2.2.2 icmp_seq=5 ttl=254 time=0.773 ms

VPCS> ping 3.3.3.2

*2.2.2.2 icmp_seq=1 ttl=254 time=0.769 ms (ICMP type:3, code:1, Destination host unreachable)
*2.2.2.2 icmp_seq=2 ttl=254 time=0.814 ms (ICMP type:3, code:1, Destination host unreachable)
*2.2.2.2 icmp_seq=3 ttl=254 time=0.733 ms (ICMP type:3, code:1, Destination host unreachable)
*2.2.2.2 icmp_seq=4 ttl=254 time=0.830 ms (ICMP type:3, code:1, Destination host unreachable)
*2.2.2.2 icmp_seq=5 ttl=254 time=0.779 ms (ICMP type:3, code:1, Destination host unreachable)
```

SW29
```
SW29#ping 2.2.2.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2.2.2.2, timeout is 2 seconds:
U.U.U
Success rate is 0 percent (0/5)
SW29#ping 3.3.3..2
% Unrecognized host or address, or protocol not running.

SW29#ping 3.3.3.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 3.3.3.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
```

### 3. Настроим отслеживание линка через технологию IP SLA.(только для IPv4):

- Пусть будет маршрут через интерфейс e0/1 роутера R28 приоритетнее. Для этого настроим отслеживание IP-адреса 10.64.52.1 (интерфейса e0/1 на роутере R23).
- Создадим статический маршрут к сети 10.64.52.0/30 и включим технологию IP SLA, а также применим ее к маршруту добавленного ранее:

```
R28#sh run | sec ip route
ip route 10.64.52.0 255.255.255.252 2.2.2.2 track 1
ip route 10.64.52.0 255.255.255.252 3.3.3.2 10
!
R28#sh run | sec sla
track 1 ip sla 1 reachability
 delay down 10 up 5
ip sla 1
 icmp-echo 2.2.2.2 source-ip 2.2.2.1
 threshold 1000
 timeout 1500
 frequency 3
ip sla schedule 1 life forever start-time now
```

### 4. Настроим для офиса Лабытнанги маршрут по-умолчанию и задокументируем все изменения:

- Создадим *route-map* default-route которая будет весь трафик отправлять на интерфейс e0/0 роутера R27:

```
R27#sh route-map
route-map default-route, permit, sequence 10
  Match clauses:
    interface Ethernet0/0
  Set clauses:
    ip next-hop 1.1.1.2
  Policy routing matches: 0 packets, 0 bytes
!
R27#sh run inter e0/0
Building configuration...

Current configuration : 174 bytes
!
interface Ethernet0/0
 description l3:to-AS-520
 ip address 1.1.1.1 255.255.255.252
 ipv6 address FE80::1 link-local
 ipv6 address 2000:0:520:1111::1/112
 ipv6 enable
end
```

Все изменения приведены [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_05/Configs)
