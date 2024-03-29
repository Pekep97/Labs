# Основные протоколы сети интернет

### Задание:


1. Настроить DHCP в офисе Москва;
2. Настроить синхронизацию времени в офисе Москва;
3. Настроить NAT в офисе Москва, C.-Перетбруг и Чокурдах.

  ### Решение:

1. [Настроим NAT(PAT) на R14 и R15. Трансляция осуществляется в адрес автономной системы AS1001;](https://github.com/Pekep97/Labs/tree/main/Lab_12#1-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-natpat-%D0%BD%D0%B0-r14-%D0%B8-r15-%D1%82%D1%80%D0%B0%D0%BD%D1%81%D0%BB%D1%8F%D1%86%D0%B8%D1%8F-%D0%BE%D1%81%D1%83%D1%89%D0%B5%D1%81%D1%82%D0%B2%D0%BB%D1%8F%D0%B5%D1%82%D1%81%D1%8F-%D0%B2-%D0%B0%D0%B4%D1%80%D0%B5%D1%81-%D0%B0%D0%B2%D1%82%D0%BE%D0%BD%D0%BE%D0%BC%D0%BD%D0%BE%D0%B9-%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B-as1001)
2. [Настроим NAT(PAT) на R18. Трансляция осуществляется в пул из 5 адресов автономной системы AS2042;](https://github.com/Pekep97/Labs/tree/main/Lab_12#2-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-natpat-%D0%BD%D0%B0-r18-%D1%82%D1%80%D0%B0%D0%BD%D1%81%D0%BB%D1%8F%D1%86%D0%B8%D1%8F-%D0%BE%D1%81%D1%83%D1%89%D0%B5%D1%81%D1%82%D0%B2%D0%BB%D1%8F%D0%B5%D1%82%D1%81%D1%8F-%D0%B2-%D0%BF%D1%83%D0%BB-%D0%B8%D0%B7-5-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%BE%D0%B2-%D0%B0%D0%B2%D1%82%D0%BE%D0%BD%D0%BE%D0%BC%D0%BD%D0%BE%D0%B9-%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B-as2042)
3. [Настроим статический NAT для R20;](https://github.com/Pekep97/Labs/tree/main/Lab_12#3-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D1%81%D1%82%D0%B0%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9-nat-%D0%B4%D0%BB%D1%8F-r20)
4. [Настроим NAT так, чтобы R19 был доступен с любого узла для удаленного управления;](https://github.com/Pekep97/Labs/tree/main/Lab_12#4-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-nat-%D1%82%D0%B0%D0%BA-%D1%87%D1%82%D0%BE%D0%B1%D1%8B-r19-%D0%B1%D1%8B%D0%BB-%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%B5%D0%BD-%D1%81-%D0%BB%D1%8E%D0%B1%D0%BE%D0%B3%D0%BE-%D1%83%D0%B7%D0%BB%D0%B0-%D0%B4%D0%BB%D1%8F-%D1%83%D0%B4%D0%B0%D0%BB%D0%B5%D0%BD%D0%BD%D0%BE%D0%B3%D0%BE-%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F)
  - 4*. [Настроим статический NAT(PAT) для офиса Чокурдах;](https://github.com/Pekep97/Labs/tree/main/Lab_12#4-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D1%81%D1%82%D0%B0%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9-natpat-%D0%B4%D0%BB%D1%8F-%D0%BE%D1%84%D0%B8%D1%81%D0%B0-%D1%87%D0%BE%D0%BA%D1%83%D1%80%D0%B4%D0%B0%D1%85)
5. [Настроим для IPv4 DHCP сервер в офисе Москва на маршрутизаторах R12 и R13. VPC1 и VPC7 получают сетевые настройки по DHCP;](https://github.com/Pekep97/Labs/tree/main/Lab_12#5-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%B4%D0%BB%D1%8F-ipv4-dhcp-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80-%D0%B2-%D0%BE%D1%84%D0%B8%D1%81%D0%B5-%D0%BC%D0%BE%D1%81%D0%BA%D0%B2%D0%B0-%D0%BD%D0%B0-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80%D0%B0%D1%85-r12-%D0%B8-r13-vpc1-%D0%B8-vpc7-%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B0%D1%8E%D1%82-%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D1%8B%D0%B5-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B8-%D0%BF%D0%BE-dhcp)
6. [Настроим NTP сервер на R12 и R13. Все устройства в офисе Москва синхронизируют время с R12 и R13;](https://github.com/Pekep97/Labs/tree/main/Lab_12#6-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-ntp-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80-%D0%BD%D0%B0-r12-%D0%B8-r13-%D0%B2%D1%81%D0%B5-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2%D0%B0-%D0%B2-%D0%BE%D1%84%D0%B8%D1%81%D0%B5-%D0%BC%D0%BE%D1%81%D0%BA%D0%B2%D0%B0-%D1%81%D0%B8%D0%BD%D1%85%D1%80%D0%BE%D0%BD%D0%B8%D0%B7%D0%B8%D1%80%D1%83%D1%8E%D1%82-%D0%B2%D1%80%D0%B5%D0%BC%D1%8F-%D1%81-r12-%D0%B8-r13)
7. [Проверим все сети в лабораторной работе на IP связность и задокументируем все изменения.](https://github.com/Pekep97/Labs/tree/main/Lab_12#7-%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%B8%D0%BC-%D0%B2%D1%81%D0%B5-%D1%81%D0%B5%D1%82%D0%B8-%D0%B2-%D0%BB%D0%B0%D0%B1%D0%BE%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BD%D0%BE%D0%B9-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B5-%D0%BD%D0%B0-ip-%D1%81%D0%B2%D1%8F%D0%B7%D0%BD%D0%BE%D1%81%D1%82%D1%8C-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)

### 1. Настроим NAT(PAT) на R14 и R15. Трансляция осуществляется в адрес автономной системы AS1001:

- Исследуемая схема описана [тут.](https://github.com/Pekep97/Labs/tree/main/Lab_04) Для упрощения понимания задублируем в этой работе только нужное:

### Исследуемая схема:

![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_12/Lab_12.png)

### Таблица адресного пространства:

|              |            |                 | *Москва*        |                       |             |                     |             |                |
|--------------|------------|-----------------|---------------|-----------------------|-------------|---------------------|-------------|----------------|
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address        | IPv6-prefix | LLIPv6-address |
| R12          | e0/0.100   | MANAGEMENT_MSK  | 10.58.100.2   | 255.255.255.0 (/24)   | -           | fd00:10:58:100::1   | /64         | fe80::1        |
|              | e0/1.10    | DHCP_MSK        | 192.168.10.3  | 255.255.255.0 (/24)   | -           | fd00:192:168:10::1  | /64         | fe80::1        |
|              | e0/2       | l3:to-R14       | 10.64.100.1   | 255.255.255.252 (/30) | -           | fd00:0:12:14::1     | /112        | fe80::1        |
|              | e0/3       | l3:to-R15       | 10.64.100.5   | 255.255.255.252 (/30) | -           | fd00:0:12:15::1     | /112        | fe80::1        |
|              | Loopback0  | -               | 172.16.255.12   | 255.255.255.255(/32)  | -           |   |         |         |
| R13          | e0/0.100   | MANAGEMENT_MSK  | 10.58.100.4   | 255.255.255.0 (/24)   | -           | fd00:10:58:100::1   | /64         | fe80::100      |
|              | e0/1.10    | DHCP_MSK        | 192.168.10.5  | 255.255.255.0 (/24)   | -           | fd00:192:168:10::1  | /64         | fe80::10       |
|              | e0/2       | l3:to-R15       | 10.64.100.13  | 255.255.255.252 (/30) | -           | fd00:0:13:15::1     | /112        | fe80::1        |
|              | e0/3       | l3:to-R14       | 10.64.100.9   | 255.255.255.252 (/30) | -           | fd00:0:13:14::1     | /112        | fe80::1        |
|              | Loopback0  | -               | 172.16.255.13   | 255.255.255.255(/32)  | -           |   |         |         |
| VRRP_R12+R13 | -          | MANAGEMENT_MSK  | 10.58.100.1   | 255.255.255.0 (/24)   | -           | -                   | -           | -              |
|              | -          | DHCP_MSK        | 192.168.10.1  | 255.255.255.0 (/24)   | -           | -                   | -           | -              |
| R14          | e0/0       | l3:to-R12       | 10.64.100.2   | 255.255.255.252 (/30) | -           | fd00:0:12:14::2     | /112        | fe80::2        |
|              | e0/1       | l3:to-R13       | 10.64.100.13  | 255.255.255.252 (/30) | -           | fd00:0:13:14::2     | /112        | fe80::2        |
|              | e0/2       | l3:to-AS-101    | 85.10.22.2    | 255.255.255.252 (/30) | -           | 2000:0:1001:101::2  | /112        | fe80::2        |
|              | e0/3       | l3:to-R19       | 10.64.100.21  | 255.255.255.252 (/30) | -           | fd00:0:14:19::1     | /112        | fe80::2        |
|              | Loopback0  | -               | 172.16.255.14   | 255.255.255.255(/32)  | -           | fd00:172:16:255::14   | /128        | fe80::1        |
|              | Loopback1  | to_NAT               | 49.28.35.14   | 255.255.255.0(/24)  | -           |   |         |         |
| R15          | e0/0       | l3:to-R13       | 10.64.100.14  | 255.255.255.252 (/30) | -           | fd00:0:13:15::2     | /112        | fe80::2        |
|              | e0/1       | l3:to-R12       | 10.64.100.6   | 255.255.255.252 (/30) | -           | fd00:0:12:15::2     | /112        | fe80::2        |
|              | e0/2       | l3:to-AS-301    | 132.50.21.2   | 255.255.255.252 (/30) | -           | 2000:0:1001:301::2  | /112        | fe80::2        |
|              | e0/3       | l3:to-R20       | 10.64.100.17  | 255.255.255.252 (/30) | -           | fd00:0:15:20::1     | /112        | fe80::2        |
|              | Loopback0  | -               | 172.16.255.15   | 255.255.255.255(/32)  | -           | fd00:172:16:255::15   | /128        | fe80::1        |
|              | Loopback1  | to_NAT               | 37.85.13.15   | 255.255.255.0(/24)  | -           |   |         |         |
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
|              | Loopback0  | -               | 172.16.255.23   | 255.255.255.255(/32)  | -           | fd00:172:16:255::23   | /128        | fe80::1        |
| R24          | e0/0       | l3:to-AS-301    | 24.100.40.1   | 255.255.255.252 (/30) | -           | 2000:0:520:301::1   | /112        | fe80::2        |
|              | e0/1       | l3:to-R26       | 10.64.52.9    | 255.255.255.252 (/30) | -           | fd00:0:24:26::1     | /112        | fe80::2        |
|              | e0/2       | l3:to-R23       | 10.64.52.6    | 255.255.255.252 (/30) | -           | fd00:0:23:24::2     | /112        | fe80::2        |
|              | e0/3       | l3:to-AS-2042   | 24.100.40.5   | 255.255.255.252 (/30) | -           | 2000:0:520:2042::1  | /112        | fe80::2        |
|              | Loopback0  | -               | 172.16.255.24   | 255.255.255.255(/32)  | -           | fd00:172:16:255::24   | /128        | fe80::1        |
| R25          | e0/0       | l3:to-R23       | 10.64.52.2    | 255.255.255.252 (/30) | -           | fd00:0:23:25::2     | /112        | fe80::2        |
|              | e0/1       | l3:to-LBTNG     | 1.1.1.2       | 255.255.255.252 (/30) | -           | 2000:0:520:1111::2  | /112        | fe80::2        |
|              | e0/2       | l3:to-R26       | 10.64.52.13   | 255.255.255.252 (/30) | -           | fd00:0:25:26::1     | /112        | fe80::2        |
|              | e0/3       | l3:to-CHKR      | 2.2.2.2       | 255.255.255.252 (/30) | -           | 2000:0:520:2222::2  | /112        | fe80::2        |
|              | Loopback0  | -               | 172.16.255.25   | 255.255.255.255(/32)  | -           | fd00:172:16:255::25   | /128        | fe80::1        |
| R26          | e0/0       | l3:to-R24       | 10.64.52.10   | 255.255.255.252 (/30) | -           | fd00:0:24:26::2     | /112        | fe80::1        |
|              | e0/1       | l3:to-CHKR      | 3.3.3.2       | 255.255.255.252 (/30) | -           | 2000:0:520:3333::2  | /112        | fe80::1        |
|              | e0/2       | l3:to-R25       | 10.64.52.14   | 255.255.255.252 (/30) | -           | fd00:0:25:26::2     | /112        | fe80::1        |
|              | e0/3       | l3:to-AS-2042   | 26.100.40.1   | 255.255.255.252 (/30) | -           | 2000:0:2042:520::1  | /112        | fe80::1        |
|              | Loopback0  | -               | 172.16.255.26   | 255.255.255.255(/32)  | -           | fd00:172:16:255::26   | /128        | fe80::1        |
|              |            |                 | *Лабытнанги*    |                       |             |                     |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address        | IPv6-prefix | LLIPv6-address |
| R27          | e0/0       | l3:to-AS-520    | 1.1.1.1       | 255.255.255.252 (/30) | -           | 2000:0:520:1111::1  | /112        | fe80::1        |
|              | Loopback0  | -               | 172.16.255.27   | 255.255.255.255(/32)  | -           | fd00:172:16:255::27   | /128        | fe80::1        |
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
|              | Loopback1  | to_NAT               | 53.17.29.18   | 255.255.255.0(/24)  | -           |   |         |         |
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
|              | Loopback0  | -               | 172.16.255.28   | 255.255.255.255(/32)  | -           | fd00:172:16:255::28   | /128        | fe80::1     
|              | Loopback1  | to_NAT               | 63.47.15.28   | 255.255.255.0(/24)  | -           |   |         |         |
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

- Создадим интерфейс ***Loopback1*** и назначим IP-адреса согласно [таблице](https://github.com/Pekep97/Labs/blob/main/Lab_12/README.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%BD%D0%BE%D0%B3%D0%BE-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%B0), через который будем реализовывать NAT(PAT) на R14 и R15; для реализации отказоустойчивости, добавим назначенные сети в eBGP протокол офиса Москва и удалим сеть ***192.168.10.0/24*** из протокола.
- Настроим NAT, eBGP в офисе Москва на R14 и R15 с учетом новых сетей, покажем настройку на R15:

***R15***
```
R15#sh run | sec access-list

ip access-list standard NAT
 permit 192.168.10.0 0.0.0.255

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R15#sh run | sec nat

ip nat source list NAT interface Loopback1 overload

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R15#sh run inter e0/0
Building configuration...

Current configuration : 274 bytes
!
interface Ethernet0/0
 description l3:to-R13
 ip address 10.64.100.14 255.255.255.252
 ip nat enable
 ip ospf network point-to-point
 ipv6 address FE80::2 link-local
 ipv6 address FD00:0:13:15::2/112
 ipv6 enable
 ipv6 ospf 1 area 0
 ipv6 ospf network point-to-point
end

R15#sh run inter e0/1
Building configuration...

Current configuration : 273 bytes
!
interface Ethernet0/1
 description l3:to-R12
 ip address 10.64.100.6 255.255.255.252
 ip nat enable
 ip ospf network point-to-point
 ipv6 address FE80::2 link-local
 ipv6 address FD00:0:12:15::2/112
 ipv6 enable
 ipv6 ospf 1 area 0
 ipv6 ospf network point-to-point
end

R15#sh run inter e0/2
Building configuration...

Current configuration : 193 bytes
!
interface Ethernet0/2
 description l3:to-AS-301
 ip address 132.50.21.2 255.255.255.252
 ip nat enable
 ipv6 address FE80::2 link-local
 ipv6 address 2000:0:1001:301::2/112
 ipv6 enable
end

R15#sh run inter l1
Building configuration...

Current configuration : 100 bytes
!
interface Loopback1
 description to_NAT
 ip address 37.85.13.15 255.255.255.0
 ip nat enable
end

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R15#sh run | sec bgp
router bgp 1001
 bgp router-id 15.15.15.15
 bgp log-neighbor-changes
 neighbor 2000:0:1001:301::1 remote-as 301
 neighbor 132.50.21.1 remote-as 301
 neighbor 172.16.255.14 remote-as 1001
 neighbor FD00:172:16:255::14 remote-as 1001
 !
 address-family ipv4
  network 10.58.100.0 mask 255.255.255.0
  network 10.64.100.0 mask 255.255.255.252
  network 10.64.100.4 mask 255.255.255.252
  network 10.64.100.8 mask 255.255.255.252
  network 10.64.100.12 mask 255.255.255.252
  network 10.64.100.16 mask 255.255.255.252
  network 10.64.100.20 mask 255.255.255.252
  network 37.85.13.0 mask 255.255.255.0
  network 132.50.21.0 mask 255.255.255.252
  network 172.16.255.15 mask 255.255.255.255
  no neighbor 2000:0:1001:301::1 activate
  neighbor 132.50.21.1 activate
  neighbor 132.50.21.1 next-hop-self
  neighbor 132.50.21.1 soft-reconfiguration inbound
  neighbor 132.50.21.1 route-map LP_200 in
  neighbor 132.50.21.1 filter-list 1 out
  neighbor 172.16.255.14 activate
  neighbor 172.16.255.14 next-hop-self
  no neighbor FD00:172:16:255::14 activate
 exit-address-family
 !
 address-family ipv6
  network 2000:0:1001:301::/112
  network FD00:0:12:14::/112
  network FD00:0:12:15::/112
  network FD00:0:13:14::/112
  network FD00:0:13:15::/112
  network FD00:0:14:19::/112
  network FD00:0:15:20::/112
  network FD00:10:58:100::/64
  network FD00:172:16:255::15/128
  network FD00:192:168:10::/64
  neighbor 2000:0:1001:301::1 activate
  neighbor 2000:0:1001:301::1 next-hop-self
  neighbor 2000:0:1001:301::1 soft-reconfiguration inbound
  neighbor 2000:0:1001:301::1 route-map LP_200 in
  neighbor 2000:0:1001:301::1 filter-list 1 out
  neighbor FD00:172:16:255::14 activate
  neighbor FD00:172:16:255::14 next-hop-self
 exit-address-family
```

- Проверим работу NAT пропинговав с VPC1 адрес, который находится за пределами  AS1001, например (IPv4 23.100.40.1) и показав статистику NAT-трансляций на R15:

***VPC1***
```
VPCS> sh ip

NAME        : VPCS[1]
IP/MASK     : 192.168.10.10/24
GATEWAY     : 192.168.10.1
DNS         : 192.168.10.1
DHCP SERVER : 192.168.10.5
DHCP LEASE  : 217526, 217800/108900/190575
DOMAIN NAME : DHCP_MSK.com
MAC         : 00:50:79:66:68:01
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:30000
MTU         : 1500

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

VPCS> ping 23.100.40.1

84 bytes from 23.100.40.1 icmp_seq=1 ttl=249 time=2.165 ms
84 bytes from 23.100.40.1 icmp_seq=2 ttl=249 time=2.565 ms
84 bytes from 23.100.40.1 icmp_seq=3 ttl=249 time=2.502 ms
84 bytes from 23.100.40.1 icmp_seq=4 ttl=249 time=2.143 ms
84 bytes from 23.100.40.1 icmp_seq=5 ttl=249 time=2.247 ms
```

***R15***
```
R15#sh ip nat nvi translations
Pro Source global      Source local       Destin  local      Destin  global
udp 37.85.13.15:9200   192.168.10.10:9200 23.100.40.1:9201   23.100.40.1:9201
udp 37.85.13.15:42384  192.168.10.10:42384 23.100.40.1:42385 23.100.40.1:42385
```

### 2. Настроим NAT(PAT) на R18. Трансляция осуществляется в пул из 5 адресов автономной системы AS2042:

- Создадим интерфейс ***Loopback1*** и назначим IP-адрес согласно [таблице](https://github.com/Pekep97/Labs/blob/main/Lab_12/README.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%BD%D0%BE%D0%B3%D0%BE-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%B0), для возможности транслировать назначенную сеть в eBGP протокол офиса С.-Петербург и удалим сеть ***192.168.20.0/24*** из протокола.
- Создадим ***nat-pool*** в который добавим 5 адресов (53.17.29.1...5), они будут использоваться для NAT-ирования сети ***192.168.20.0/24*** которую укажем в ***access-list***;
- Настроим NAT, eBGP в офисе С.-Петербург на R18 с учетом новой сети, покажем настройку на R18:

***R18***
```
R18#sh run | sec ip nat pool
ip nat pool PAT 53.17.29.1 53.17.29.5 netmask 255.255.255.0

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R18#sh run | sec access-list
ip access-list standard NAT
 permit 192.168.20.0 0.0.0.255

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R18#sh run | sec nat

ip nat source list NAT pool PAT overload

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R18#sh run inter e0/0
Building configuration...

Current configuration : 186 bytes
!
interface Ethernet0/0
 description l3:to-R16
 ip address 10.64.20.5 255.255.255.252
 ip nat enable
 ipv6 address FE80::1 link-local
 ipv6 address FD00:0:16:18::1/112
 ipv6 enable
end

R18#sh run inter e0/1
Building configuration...

Current configuration : 186 bytes
!
interface Ethernet0/1
 description l3:to-R17
 ip address 10.64.20.1 255.255.255.252
 ip nat enable
 ipv6 address FE80::1 link-local
 ipv6 address FD00:0:17:18::1/112
 ipv6 enable
end

R18#sh run inter e0/2
Building configuration...

Current configuration : 190 bytes
!
interface Ethernet0/2
 description l3:to-R24
 ip address 24.100.40.6 255.255.255.252
 ip nat enable
 ipv6 address FE80::1 link-local
 ipv6 address 2000:0:520:2042::2/112
 ipv6 enable
end

R18#sh run inter l1
Building configuration...

Current configuration : 80 bytes
!
interface Loopback1
 ip address 53.17.29.18 255.255.255.0
 ip nat enable
end

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R18#sh run | sec bgp
router bgp 2042
 bgp router-id 18.18.18.18
 bgp log-neighbor-changes
 neighbor 24.100.40.5 remote-as 520
 neighbor 26.100.40.1 remote-as 520
 neighbor 2000:0:520:2042::1 remote-as 520
 neighbor 2000:0:2042:520::1 remote-as 520
 !
 address-family ipv4
  network 10.58.200.0 mask 255.255.255.0
  network 10.64.20.0 mask 255.255.255.252
  network 10.64.20.4 mask 255.255.255.252
  network 10.64.20.8 mask 255.255.255.252
  network 24.100.40.4 mask 255.255.255.252
  network 26.100.40.0 mask 255.255.255.252
  network 53.17.29.0 mask 255.255.255.0
  neighbor 24.100.40.5 activate
  neighbor 24.100.40.5 next-hop-self
  neighbor 24.100.40.5 prefix-list DENY_TRANSIT out
  neighbor 26.100.40.1 activate
  neighbor 26.100.40.1 next-hop-self
  neighbor 26.100.40.1 prefix-list DENY_TRANSIT out
  no neighbor 2000:0:520:2042::1 activate
  no neighbor 2000:0:2042:520::1 activate
  maximum-paths 2
 exit-address-family
 ```

- Проверим работу NAT пропинговав с VPC8 адрес, который находится за пределами  AS2042, например (IPv4 23.100.40.1) и показав статистику NAT-трансляций на R18:

***VPC8***
```
VPCS> ping 23.100.40.1

84 bytes from 23.100.40.1 icmp_seq=1 ttl=252 time=1.406 ms
84 bytes from 23.100.40.1 icmp_seq=2 ttl=252 time=1.601 ms
84 bytes from 23.100.40.1 icmp_seq=3 ttl=252 time=1.702 ms
84 bytes from 23.100.40.1 icmp_seq=4 ttl=252 time=1.431 ms
84 bytes from 23.100.40.1 icmp_seq=5 ttl=252 time=1.665 ms
```

***R18***
```
R18#sh ip nat nvi translations
Pro Source global      Source local       Destin  local      Destin  global
icmp 53.17.29.1:5289   192.168.20.6:5289  23.100.40.1:5289   23.100.40.1:5289
icmp 53.17.29.1:5545   192.168.20.6:5545  23.100.40.1:5545   23.100.40.1:5545
icmp 53.17.29.1:5801   192.168.20.6:5801  23.100.40.1:5801   23.100.40.1:5801

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R18#sh ip nat nvi statistics
Total active translations: 5 (0 static, 5 dynamic; 5 extended)
NAT Enabled interfaces:
  Ethernet0/0, Ethernet0/1, Ethernet0/2, Loopback1
Hits: 17  Misses: 20
CEF Translated packets: 20, CEF Punted packets: 0
Expired translations: 15
Dynamic mappings:
-- Source [Id: 1] access-list NAT pool PAT refcount 5
 pool PAT: netmask 255.255.255.0
        start 53.17.29.1 end 53.17.29.5
        type generic, total addresses 5, allocated 1 (20%), misses 0
```

### 3. Настроим статический NAT для R20:

- Настроим статический NAT на маршрутизаторах R14, R15 через IP-адреса ***37.85.13.20*** и ***49.28.35.20 для IP-адреса ***10.64.100.18*** (предварительно удалив эту сеть из протокола BGPна R14, R15), который принадлежит интерфейсу маршрутизатора ***R20***, покажем настройку на R15:

***R15***
```
R15(config)#ip nat source static 10.64.100.18 37.85.13.20
```

- Проверим работу NAT пропинговав с R20 адрес, который находится за пределами  AS1001, например (IPv4 23.100.40.1) и показав статистику NAT-трансляций на R15:

***R20***
```
R20#ping 23.100.40.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 23.100.40.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
```

***R15***
```
R15#sh ip nat nvi translations
Pro Source global      Source local       Destin  local      Destin  global
icmp 37.85.13.20:2     10.64.100.18:2     23.100.40.1:2      23.100.40.1:2
--- 37.85.13.20        10.64.100.18       ---                ---
tcp 37.85.13.22:22     10.64.100.22:22    ---                ---
```

### 4. Настроим NAT так, чтобы R19 был доступен с любого узла для удаленного управления;

- Настроим на R19 возможность подключения по SSH:

***R19***
```
hostname R19
!
enable secret 5 $1$/yqZ$WE/0YR0XnODtDBsZeUD1j/
!
aaa new-model
!
ip domain name OTUS
!
username admin privilege 15 secret 5 $1$U/Md$PI1HGnXQGVMa2VSKDea6M.
!
ip ssh version 2
!
line vty 0 2
 password cisco
 transport input ssh
```

- На R14, R15 настроим статический NAT с IP-адресов ***49.28.35.22***, ***37.85.13.22*** с пробросом порта SSH (22) на ***10.64.100.22***;
- Покажем настройку на R15:

***R15***
```
ip nat source static tcp 10.64.100.22 22 37.85.13.22 22 extendable
```

- Проверим работу NAT пропинговав IP-адреса  ***49.28.35.22***, ***37.85.13.22*** с R27 (результат должнен быть отрицателен для IP ***49.28.35.22*** пока есть в сети R15, так как он настроен приоритетным в AS1001), а затем подключимся к этим адресам через SSH с маршрутизатора R27 (результат должнен быть отрицателен для IP ***49.28.35.22*** пока есть в сети R15, так как он настроен приоритетным в AS1001):

***R27***
```
R27#ping 37.85.13.22
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 37.85.13.22, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
!
R27#ping 49.28.35.22
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 49.28.35.22, timeout is 2 seconds:
.....
Success rate is 0 percent (0/5)
!
R27#ssh 37.85.13.22
Password:
 unauthorized access prohibited
R19>exit
!
[Connection to 37.85.13.22 closed by foreign host]
R27#ssh 49.28.35.22
R27#
```
- Покажем NAT-трансляции на R15:

***R15***
```
R15#sh ip nat nvi translations
Pro Source global      Source local       Destin  local      Destin  global
tcp 1.1.1.1:39191      1.1.1.1:39191      37.85.13.22:22     10.64.100.22:22
--- 37.85.13.20        10.64.100.18       ---                ---
tcp 37.85.13.22:22     10.64.100.22:22    ---                ---
```

### 4*. Настроим статический NAT(PAT) для офиса Чокурдах:

- Для реализации требуется выполнить следующеее:
    * Создать интерфейс ***Loopback1*** и назначить IP-адрес согласно [таблице](https://github.com/Pekep97/Labs/blob/main/Lab_12/README.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%BD%D0%BE%D0%B3%D0%BE-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%B0), для возможности транслировать назначенную сеть в eBGP протокол офиса Чокурдах и удалить сеть ***192.168.100.0/24*** из протокола;
    * Организовать статическую привязку IP-адресов ***192.168.100.30*** и ***192.168.100.31*** для VPC30, VPC31 соответственно, на DHCP-сервере маршрутизатора R28;
    * Создать ***acess-list*** - ы которые разрешают только указанные выше IP-адреса;
    * Создать ***nat-pool*** - ы в которых объявим IP-адреса ***63.47.15.30*** и ***63.47.15.31*** которыми будем натить IP-адреса ***192.168.100.30*** и ***192.168.100.31*** соответственно;
    * Настроить PAT на R28 с учетом выше указанных переменных.

***R28***
```
R28#sh run inter l1 // Создаtv интерфейс ***Loopback1*** и назначаем IP-адрес
!
interface Loopback1
 description to_NAT
 ip address 63.47.15.28 255.255.255.0
 ip nat enable
end
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
R28#sh run | sec dhcp // Организовываем статическую привязку IP-адресов ***192.168.100.30*** и ***192.168.100.31*** для VPC30, VPC31 соответственно, на DHCP-сервере маршрутизатора R28
ip dhcp excluded-address 192.168.100.1 192.168.100.5
ip dhcp pool DHCP_CHKR
 network 192.168.100.0 255.255.255.0
 default-router 192.168.100.1
 dns-server 192.168.100.1
 domain-name DHCP_CHKR.com
 lease 2 12 30
ip dhcp pool VPC30
 host 192.168.100.30 255.255.255.0
 client-identifier 0100.5079.6668.1e
ip dhcp pool VPC31
 host 192.168.100.31 255.255.255.0
 client-identifier 0100.5079.6668.1f
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
R28#sh run | sec access-list // Создаем ***acess-list*** - ы которые разрешают только указанные выше IP-адреса
ip access-list standard VPC30
 permit 192.168.100.30
ip access-list standard VPC31
 permit 192.168.100.31
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
R28#sh run | sec pool // Создаем ***nat-pool*** - ы в которых объявим IP-адреса ***63.47.15.30*** и ***63.47.15.31*** которыми будем натить IP-адреса ***192.168.100.30*** и ***192.168.100.31*** соответственно
ip nat pool VPC30 63.47.15.30 63.47.15.30 netmask 255.255.255.0
ip nat pool VPC31 63.47.15.31 63.47.15.31 netmask 255.255.255.0
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
R28#sh run | sec nat //  Настроим PAT на R28 с учетом выше указанных переменных
R28#sh run  inter e0/0
!
interface Ethernet0/0
 description l3:to-AS-520
 ip address 3.3.3.1 255.255.255.252
 ip nat enable
 ipv6 address FE80::2 link-local
 ipv6 address 2000:0:520:3333::1/112
 ipv6 enable
end
!
R28#sh run  inter e0/1
!
interface Ethernet0/1
 description l3:to-AS-520
 ip address 2.2.2.1 255.255.255.252
 ip nat enable
 ipv6 address FE80::1 link-local
 ipv6 address 2000:0:520:2222::1/112
 ipv6 enable
end
!
R28#sh run  inter e0/2.10
!
interface Ethernet0/2.10
 description DHCP_CHKR
 encapsulation dot1Q 10
 ip address 192.168.100.1 255.255.255.0
 ip nat enable
 ip policy route-map permit_to-R25
 ipv6 address FE80::1 link-local
 ipv6 address FD00:192:168:100::1/64
 ipv6 enable
end
!
ip nat pool VPC30 63.47.15.30 63.47.15.30 netmask 255.255.255.0
ip nat pool VPC31 63.47.15.31 63.47.15.31 netmask 255.255.255.0
```

### 5. Настроим для IPv4 DHCP сервер в офисе Москва на маршрутизаторах R12 и R13. VPC1 и VPC7 получают сетевые настройки по DHCP:

Описание процесса указано [тут.](https://github.com/Pekep97/Labs/tree/main/Lab_04#5-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D1%81%D0%B5%D1%82%D0%B8-%D0%BE%D1%84%D0%B8%D1%81%D0%BE%D0%B2-%D1%82%D0%B0%D0%BA-%D1%87%D1%82%D0%BE%D0%B1%D1%8B-%D0%BD%D0%B5-%D0%B2%D0%BE%D0%B7%D0%BD%D0%B8%D0%BA%D0%B0%D0%BB%D0%BE-broadcast-%D1%88%D1%82%D0%BE%D1%80%D0%BC%D0%BE%D0%B2-%D0%B0-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BB%D0%B8%D0%BD%D0%BA%D0%BE%D0%B2-%D0%B1%D1%8B%D0%BB%D0%BE-%D0%BC%D0%B0%D0%BA%D1%81%D0%B8%D0%BC%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE-%D0%BE%D0%BF%D1%82%D0%B8%D0%BC%D0%B8%D0%B7%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BE-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)

### 6. Настроим NTP сервер на R12 и R13. Все устройства в офисе Москва синхронизируют время с R12 и R13:

- Создадим интерфейс ***Loopback0*** на R12 и R13 и назначим IP-адреса согласно [таблице](https://github.com/Pekep97/Labs/blob/main/Lab_12/README.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%BD%D0%BE%D0%B3%D0%BE-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%B0), который будем использовать в качестве NTP-сервера и покажем настройку на R13:

***R13***
```
R13#sh run inter l0
!
interface Loopback0
 ip address 172.16.255.13 255.255.255.255
end
!!!!!!!!!!!!!!!!!!!!!!
R13#sh run | sec ntp
ntp logging
ntp source Loopback0
ntp master 13
ntp update-calendar
```

- Настроим все остальные устройства в качестве клиентов, покажем пример настройки на SW2:

***SW2***
```
SW2#sh run | sec ntp
ntp server 172.16.255.12 source Vlan100
ntp server 172.16.255.13 source Vlan100
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
SW2#sh ntp associations

  address         ref clock       st   when   poll reach  delay  offset   disp
+~172.16.255.12   127.127.1.1     12     51     64    77  1.000   0.500  2.925
*~172.16.255.13   127.127.1.1     13     55     64    77  1.000   0.500  2.898
 * sys.peer, # selected, + candidate, - outlyer, x falseticker, ~ configured
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
SW2#sh clock detail
*15:07:59.513 MSK Wed Feb 21 2024
Time source is NTP
```

### 7. Проверим все сети в лабораторной работе на IP связность и задокументируем все изменения:

- Продемонстрируем IP-связность показав полную таблицу маршрутизации на R27, так как он наиболее отдален от всех AS:

***R27_IPv4***
```
R27#sh ip rou bgp
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

      2.0.0.0/30 is subnetted, 1 subnets
B        2.2.2.0 [20/0] via 1.1.1.2, 2w6d
      3.0.0.0/30 is subnetted, 1 subnets
B        3.3.3.0 [20/0] via 1.1.1.2, 2w6d
      10.0.0.0/8 is variably subnetted, 14 subnets, 2 masks
B        10.58.10.0/24 [20/0] via 1.1.1.2, 04:20:53
B        10.58.100.0/24 [20/0] via 1.1.1.2, 00:30:42
B        10.58.200.0/24 [20/0] via 1.1.1.2, 22:54:01
B        10.64.20.0/30 [20/0] via 1.1.1.2, 22:54:01
B        10.64.20.4/30 [20/0] via 1.1.1.2, 22:54:01
B        10.64.52.0/30 [20/0] via 1.1.1.2, 2w6d
B        10.64.52.4/30 [20/0] via 1.1.1.2, 2w6d
B        10.64.52.8/30 [20/0] via 1.1.1.2, 2w6d
B        10.64.52.12/30 [20/0] via 1.1.1.2, 2w6d
B        10.64.100.0/30 [20/0] via 1.1.1.2, 00:30:42
B        10.64.100.4/30 [20/0] via 1.1.1.2, 00:30:42
B        10.64.100.8/30 [20/0] via 1.1.1.2, 00:30:42
B        10.64.100.12/30 [20/0] via 1.1.1.2, 00:30:42
B        10.64.100.20/30 [20/0] via 1.1.1.2, 00:30:42
      21.0.0.0/30 is subnetted, 1 subnets
B        21.22.100.0 [20/0] via 1.1.1.2, 1d22h
      23.0.0.0/30 is subnetted, 1 subnets
B        23.100.40.0 [20/0] via 1.1.1.2, 2w6d
      24.0.0.0/30 is subnetted, 2 subnets
B        24.100.40.0 [20/0] via 1.1.1.2, 2w6d
B        24.100.40.4 [20/0] via 1.1.1.2, 2w6d
      26.0.0.0/30 is subnetted, 1 subnets
B        26.100.40.0 [20/0] via 1.1.1.2, 2w6d
      37.0.0.0/24 is subnetted, 1 subnets
B        37.85.13.0 [20/0] via 1.1.1.2, 00:30:42
      49.0.0.0/24 is subnetted, 1 subnets
B        49.28.35.0 [20/0] via 1.1.1.2, 00:30:42
      53.0.0.0/24 is subnetted, 1 subnets
B        53.17.29.0 [20/0] via 1.1.1.2, 22:54:01
      63.0.0.0/24 is subnetted, 1 subnets
B        63.47.15.0 [20/0] via 1.1.1.2, 04:20:53
      85.0.0.0/30 is subnetted, 1 subnets
B        85.10.22.0 [20/0] via 1.1.1.2, 1d22h
      132.50.0.0/30 is subnetted, 1 subnets
B        132.50.21.0 [20/0] via 1.1.1.2, 1d19h
      172.16.0.0/32 is subnetted, 8 subnets
B        172.16.255.14 [20/0] via 1.1.1.2, 00:30:42
B        172.16.255.15 [20/0] via 1.1.1.2, 00:30:42
B        172.16.255.23 [20/0] via 1.1.1.2, 2w6d
B        172.16.255.24 [20/0] via 1.1.1.2, 2w6d
B        172.16.255.25 [20/0] via 1.1.1.2, 2w6d
B        172.16.255.26 [20/0] via 1.1.1.2, 2w6d
B        172.16.255.28 [20/0] via 1.1.1.2, 04:20:53
B     192.168.100.0/24 [20/0] via 1.1.1.2, 04:20:53
```

***R27_IPv6***
```
R27#sh ipv6 rou bgp
IPv6 Routing Table - default - 37 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, HA - Home Agent, MR - Mobile Router, R - RIP
       H - NHRP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, NM - NEMO
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, la - LISP alt
       lr - LISP site-registrations, ld - LISP dyn-eid, a - Application
B   2000:0:301:101::/112 [20/0]
     via FE80::2, Ethernet0/0
B   2000:0:520:101::/112 [20/0]
     via FE80::2, Ethernet0/0
B   2000:0:520:301::/112 [20/20]
     via FE80::2, Ethernet0/0
B   2000:0:520:2042::/112 [20/20]
     via FE80::2, Ethernet0/0
B   2000:0:520:2222::/112 [20/0]
     via FE80::2, Ethernet0/0
B   2000:0:520:3333::/112 [20/10]
     via FE80::2, Ethernet0/0
B   2000:0:1001:101::/112 [20/0]
     via FE80::2, Ethernet0/0
B   2000:0:1001:301::/112 [20/0]
     via FE80::2, Ethernet0/0
B   2000:0:2042:520::/112 [20/10]
     via FE80::2, Ethernet0/0
B   FD00:0:12:14::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:12:15::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:13:14::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:13:15::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:14:19::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:15:20::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:16:18::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:17:18::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:23:24::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:23:25::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:0:24:26::/112 [20/20]
     via FE80::2, Ethernet0/0
B   FD00:0:25:26::/112 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:10:58:10::/64 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:10:58:100::/64 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:10:58:200::/64 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:172:16:255::14/128 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:172:16:255::15/128 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:172:16:255::23/128 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:172:16:255::24/128 [20/30]
     via FE80::2, Ethernet0/0
B   FD00:172:16:255::25/128 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:172:16:255::26/128 [20/20]
     via FE80::2, Ethernet0/0
B   FD00:172:16:255::28/128 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:192:168:10::/64 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:192:168:100::/64 [20/0]
     via FE80::2, Ethernet0/0
```

Все изменения задокументированы [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_12/Configs)
