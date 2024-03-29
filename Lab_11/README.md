# BGP. Фильтрация

### Задание:

1. Настроить фильтрацию в офисе Москва так, чтобы не появилось транзитного трафика(As-path);
2. Настроить фильтрацию в офисе С.-Петербург так, чтобы не появилось транзитного трафика(Prefix-list);
3. Настроить провайдера Киторн так, чтобы в офис Москва отдавался только маршрут по умолчанию;
4. Настроить провайдера Ламас так, чтобы в офис Москва отдавался только маршрут по умолчанию и префикс офиса С.-Петербург;
5. Все сети в лабораторной работе должны иметь IP связность.

### Решение:

1. [Настроим фильтрацию в офисе Москва так, чтобы не появилось транзитного трафика(As-path);](https://github.com/Pekep97/Labs/blob/main/Lab_11/README.md#%D1%80%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D0%B5)
2. [Настроим фильтрацию в офисе С.-Петербург так, чтобы не появилось транзитного трафика(Prefix-list);](https://github.com/Pekep97/Labs/blob/main/Lab_11/README.md#2-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D1%84%D0%B8%D0%BB%D1%8C%D1%82%D1%80%D0%B0%D1%86%D0%B8%D1%8E-%D0%B2-%D0%BE%D1%84%D0%B8%D1%81%D0%B5-%D1%81-%D0%BF%D0%B5%D1%82%D0%B5%D1%80%D0%B1%D1%83%D1%80%D0%B3-%D1%82%D0%B0%D0%BA-%D1%87%D1%82%D0%BE%D0%B1%D1%8B-%D0%BD%D0%B5-%D0%BF%D0%BE%D1%8F%D0%B2%D0%B8%D0%BB%D0%BE%D1%81%D1%8C-%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B8%D1%82%D0%BD%D0%BE%D0%B3%D0%BE-%D1%82%D1%80%D0%B0%D1%84%D0%B8%D0%BA%D0%B0prefix-list)
3. [Настроим провайдера Киторн так, чтобы в офис Москва отдавался только маршрут по умолчанию;](https://github.com/Pekep97/Labs/blob/main/Lab_11/README.md#3-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BF%D1%80%D0%BE%D0%B2%D0%B0%D0%B9%D0%B4%D0%B5%D1%80%D0%B0-%D0%BA%D0%B8%D1%82%D0%BE%D1%80%D0%BD-%D1%82%D0%B0%D0%BA-%D1%87%D1%82%D0%BE%D0%B1%D1%8B-%D0%B2-%D0%BE%D1%84%D0%B8%D1%81-%D0%BC%D0%BE%D1%81%D0%BA%D0%B2%D0%B0-%D0%BE%D1%82%D0%B4%D0%B0%D0%B2%D0%B0%D0%BB%D1%81%D1%8F-%D1%82%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82-%D0%BF%D0%BE-%D1%83%D0%BC%D0%BE%D0%BB%D1%87%D0%B0%D0%BD%D0%B8%D1%8E)
4. [Настроим провайдера Ламас так, чтобы в офис Москва отдавался только маршрут по умолчанию и префикс офиса С.-Петербург;](https://github.com/Pekep97/Labs/blob/main/Lab_11/README.md#4-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BF%D1%80%D0%BE%D0%B2%D0%B0%D0%B9%D0%B4%D0%B5%D1%80%D0%B0-%D0%BB%D0%B0%D0%BC%D0%B0%D1%81-%D1%82%D0%B0%D0%BA-%D1%87%D1%82%D0%BE%D0%B1%D1%8B-%D0%B2-%D0%BE%D1%84%D0%B8%D1%81-%D0%BC%D0%BE%D1%81%D0%BA%D0%B2%D0%B0-%D0%BE%D1%82%D0%B4%D0%B0%D0%B2%D0%B0%D0%BB%D1%81%D1%8F-%D1%82%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82-%D0%BF%D0%BE-%D1%83%D0%BC%D0%BE%D0%BB%D1%87%D0%B0%D0%BD%D0%B8%D1%8E-%D0%B8-%D0%BF%D1%80%D0%B5%D1%84%D0%B8%D0%BA%D1%81-%D0%BE%D1%84%D0%B8%D1%81%D0%B0-%D1%81-%D0%BF%D0%B5%D1%82%D0%B5%D1%80%D0%B1%D1%83%D1%80%D0%B3)
5. [Проверим все сети в лабораторной работе на IP связность и задокументируем все изменения.](https://github.com/Pekep97/Labs/blob/main/Lab_11/README.md#5-%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%B8%D0%BC-%D0%B2%D1%81%D0%B5-%D1%81%D0%B5%D1%82%D0%B8-%D0%B2-%D0%BB%D0%B0%D0%B1%D0%BE%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BD%D0%BE%D0%B9-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B5-%D0%BD%D0%B0-ip-%D1%81%D0%B2%D1%8F%D0%B7%D0%BD%D0%BE%D1%81%D1%82%D1%8C-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)

### 1. Настроим фильтрацию в офисе Москва так, чтобы не появилось транзитного трафика(As-path);

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
|              | Loopback0  | -               | 172.16.255.14   | 255.255.255.255(/32)  | -           | fd00:172:16:255::14   | /128        | fe80::1        |
| R15          | e0/0       | l3:to-R13       | 10.64.100.14  | 255.255.255.252 (/30) | -           | fd00:0:13:15::2     | /112        | fe80::2        |
|              | e0/1       | l3:to-R12       | 10.64.100.6   | 255.255.255.252 (/30) | -           | fd00:0:12:15::2     | /112        | fe80::2        |
|              | e0/2       | l3:to-AS-301    | 132.50.21.2   | 255.255.255.252 (/30) | -           | 2000:0:1001:301::2  | /112        | fe80::2        |
|              | e0/3       | l3:to-R20       | 10.64.100.17  | 255.255.255.252 (/30) | -           | fd00:0:15:20::1     | /112        | fe80::2        |
|              | Loopback0  | -               | 172.16.255.15   | 255.255.255.255(/32)  | -           | fd00:172:16:255::15   | /128        | fe80::1        |
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
|              | Loopback0  | -               | 172.16.255.28   | 255.255.255.255(/32)  | -           | fd00:172:16:255::28   | /128        | fe80::1        |
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

- Создадим ***acess-list AS-Path***, в котором разрешим передачу только пустого значения *AS-PATH*, что разрешит передачу только префиксов, порожденных в собственной AS и применим его на исходящее направление в сторону провайдеров Киторн и Ламас на маршрутизаторах R14, R15;
- Покажем пример конфигурации на R14:

***R14***
```
R14#sh run | sec access-list
ip as-path access-list 1 permit ^$
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
R14#sh run | sec bgp
router bgp 1001
 bgp router-id 14.14.14.14
 bgp log-neighbor-changes
 neighbor 2000:0:1001:101::1 remote-as 101
 neighbor 85.10.22.1 remote-as 101
 neighbor 172.16.255.15 remote-as 1001
 neighbor 172.16.255.15 update-source Loopback0
 neighbor FD00:172:16:255::15 remote-as 1001
 neighbor FD00:172:16:255::15 update-source Loopback0
 !
 address-family ipv4
  network 10.58.100.0 mask 255.255.255.0
  network 10.64.100.0 mask 255.255.255.224
  network 10.64.100.0 mask 255.255.255.252
  network 10.64.100.4 mask 255.255.255.252
  network 10.64.100.8 mask 255.255.255.252
  network 10.64.100.12 mask 255.255.255.252
  network 10.64.100.16 mask 255.255.255.252
  network 10.64.100.20 mask 255.255.255.252
  network 85.10.22.0 mask 255.255.255.252
  network 172.16.255.14 mask 255.255.255.255
  network 192.168.10.0
  no neighbor 2000:0:1001:101::1 activate
  neighbor 85.10.22.1 activate
  neighbor 85.10.22.1 next-hop-self
  neighbor 85.10.22.1 route-map AS_PATH_1001_x3 out
  neighbor 85.10.22.1 filter-list 1 out
  neighbor 172.16.255.15 activate
  neighbor 172.16.255.15 next-hop-self
  neighbor 172.16.255.15 soft-reconfiguration inbound
  no neighbor FD00:172:16:255::15 activate
 exit-address-family
 !
 address-family ipv6
  network 2000:0:1001:101::/112
  network FD00:0:12:14::/112
  network FD00:0:12:15::/112
  network FD00:0:13:14::/112
  network FD00:0:13:15::/112
  network FD00:0:14:19::/112
  network FD00:0:15:20::/112
  network FD00:10:58:100::/64
  network FD00:172:16:255::14/128
  network FD00:192:168:10::/64
  neighbor 2000:0:1001:101::1 activate
  neighbor 2000:0:1001:101::1 next-hop-self
  neighbor 2000:0:1001:101::1 route-map AS_PATH_1001_x3 out
  neighbor 2000:0:1001:101::1 filter-list 1 out
  neighbor FD00:172:16:255::15 activate
  neighbor FD00:172:16:255::15 next-hop-self
 exit-address-family
```

- Проверим то что выполняется фильтр:

***R14_IPv4***
```
R14#show ip bgp regexp ^$
BGP table version is 180, local router ID is 14.14.14.14
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 * i 10.58.100.0/24   172.16.255.15           20    100      0 i
 *>                   10.64.100.1             20         32768 i
 * i 10.64.100.0/30   172.16.255.15           20    100      0 i
 *>                   0.0.0.0                  0         32768 i
 * i 10.64.100.4/30   172.16.255.15            0    100      0 i
 *>                   10.64.100.1             20         32768 i
 * i 10.64.100.8/30   172.16.255.15           20    100      0 i
 *>                   0.0.0.0                  0         32768 i
 * i 10.64.100.12/30  172.16.255.15            0    100      0 i
 *>                   10.64.100.9             20         32768 i
 * i 10.64.100.16/30  172.16.255.15            0    100      0 i
 *>                   10.64.100.1             30         32768 i
 * i 10.64.100.20/30  172.16.255.15           30    100      0 i
 *>                   0.0.0.0                  0         32768 i
     Network          Next Hop            Metric LocPrf Weight Path
 *>  85.10.22.0/30    0.0.0.0                  0         32768 i
 *>i 132.50.21.0/30   172.16.255.15            0    100      0 i
 *>  172.16.255.14/32 0.0.0.0                  0         32768 i
 r>i 172.16.255.15/32 172.16.255.15            0    100      0 i
 * i 192.168.10.0     172.16.255.15           20    100      0 i
 *>                   10.64.100.1             20         32768 i
```

***R14_IPv6***
```
R14#show ip bgp ipv6 unicast regexp ^$
BGP table version is 238, local router ID is 14.14.14.14
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *>  2000:0:1001:101::/112
                       ::                       0         32768 i
 *>i 2000:0:1001:301::/112
                       FD00:172:16:255::15
                                                0    100      0 i
 * i FD00:0:12:14::/112
                       FD00:172:16:255::15
                                               20    100      0 i
 *>                   ::                       0         32768 i
 * i FD00:0:12:15::/112
                       FD00:172:16:255::15
                                                0    100      0 i
 *>                   FE80::1                 20         32768 i
 * i FD00:0:13:14::/112
     Network          Next Hop            Metric LocPrf Weight Path
                       FD00:172:16:255::15
                                               20    100      0 i
 *>                   ::                       0         32768 i
 * i FD00:0:13:15::/112
                       FD00:172:16:255::15
                                                0    100      0 i
 *>                   FE80::1                 20         32768 i
 * i FD00:0:14:19::/112
                       FD00:172:16:255::15
                                               30    100      0 i
 *>                   ::                       0         32768 i
 * i FD00:0:15:20::/112
                       FD00:172:16:255::15
                                                0    100      0 i
 *>                   FE80::1                 30         32768 i
 * i FD00:10:58:100::/64
                       FD00:172:16:255::15
                                               20    100      0 i
 *>                   FE80::1                 20         32768 i
 *>  FD00:172:16:255::14/128
                       ::                       0         32768 i
 r>i FD00:172:16:255::15/128
     Network          Next Hop            Metric LocPrf Weight Path
                       FD00:172:16:255::15
                                                0    100      0 i
 * i FD00:192:168:10::/64
                       FD00:172:16:255::15
                                               20    100      0 i
 *>                   FE80::1                 20         32768 i
```

### 2. Настроим фильтрацию в офисе С.-Петербург так, чтобы не появилось транзитного трафика(Prefix-list):

- Создадим ***prefix-list***, в котором разрешим передачу префиксов только своей AS, и применим его на исходящее направление в сторону провайдера Триада на маршрутизаторе R18;
- Покажем конфигурацию на R18:

***R18***
```
R18#sh run | sec prefix-list
  
ip prefix-list DENY_TRANSIT seq 5 permit 10.64.20.0/30
ip prefix-list DENY_TRANSIT seq 10 permit 10.64.20.4/30
ip prefix-list DENY_TRANSIT seq 15 permit 10.64.20.8/30
ip prefix-list DENY_TRANSIT seq 20 permit 10.58.200.0/24
ip prefix-list DENY_TRANSIT seq 25 permit 192.168.20.0/24

ipv6 prefix-list DENY_TRANSIT_IPv6 seq 5 permit FD00:0:16:18::/112
ipv6 prefix-list DENY_TRANSIT_IPv6 seq 10 permit FD00:0:16:32::/112
ipv6 prefix-list DENY_TRANSIT_IPv6 seq 15 permit FD00:0:17:18::/112
ipv6 prefix-list DENY_TRANSIT_IPv6 seq 20 permit FD00:10:58:200::/64
ipv6 prefix-list DENY_TRANSIT_IPv6 seq 25 permit FD00:192:168:20::/64

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

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
  network 192.168.20.0
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
 !
 address-family ipv6
  maximum-paths 2
  network 2000:0:520:2042::/112
  network 2000:0:2042:520::/112
  network FD00:0:16:18::/112
  network FD00:0:16:32::/112
  network FD00:0:17:18::/112
  network FD00:10:58:200::/64
  network FD00:192:168:20::/64
  neighbor 2000:0:520:2042::1 activate
  neighbor 2000:0:520:2042::1 next-hop-self
  neighbor 2000:0:520:2042::1 prefix-list DENY_TRANSIT_IPv6 out
  neighbor 2000:0:2042:520::1 activate
  neighbor 2000:0:2042:520::1 next-hop-self
  neighbor 2000:0:2042:520::1 prefix-list DENY_TRANSIT_IPv6 out
 exit-address-family
```

### 3. Настроим провайдера Киторн так, чтобы в офис Москва отдавался только маршрут по умолчанию:

- На маршрутизаторе R22 разрешим трансляцию в офис Москва только маршрут по-умолчанию при помощи ***prefix-list***;
- Покажем конфигурацию маршрутизатора R22:

***R22***
```
R22#sh run | sec prefix-list
  
ip prefix-list DEFAULT seq 5 permit 0.0.0.0/0
ipv6 prefix-list DEFAULT_IPv6 seq 5 permit ::/0

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R22#sh run | sec bgp
router bgp 101
 bgp router-id 22.22.22.22
 bgp log-neighbor-changes
 neighbor 21.22.100.2 remote-as 301
 neighbor 23.100.40.1 remote-as 520
 neighbor 2000:0:301:101::2 remote-as 301
 neighbor 2000:0:520:101::1 remote-as 520
 neighbor 2000:0:1001:101::2 remote-as 1001
 neighbor 85.10.22.2 remote-as 1001
 !
 address-family ipv4
  network 21.22.100.0 mask 255.255.255.252
  network 23.100.40.0 mask 255.255.255.252
  network 85.10.22.0 mask 255.255.255.252
  neighbor 21.22.100.2 activate
  neighbor 23.100.40.1 activate
  no neighbor 2000:0:301:101::2 activate
  no neighbor 2000:0:520:101::1 activate
  no neighbor 2000:0:1001:101::2 activate
  neighbor 85.10.22.2 activate
  neighbor 85.10.22.2 default-originate
  neighbor 85.10.22.2 soft-reconfiguration inbound
  neighbor 85.10.22.2 prefix-list DEFAULT out
 exit-address-family
 !
 address-family ipv6
  network 2000:0:301:101::/112
  network 2000:0:520:101::/112
  network 2000:0:1001:101::/112
  neighbor 2000:0:301:101::2 activate
  neighbor 2000:0:520:101::1 activate
  neighbor 2000:0:1001:101::2 activate
  neighbor 2000:0:1001:101::2 default-originate
  neighbor 2000:0:1001:101::2 soft-reconfiguration inbound
  neighbor 2000:0:1001:101::2 prefix-list DEFAULT_IPv6 out
 exit-address-family
```

- Для проверки покажем таблицу приходящих префиксов на маршрутизаторе R14 от R22:

***R14_IPv4***
```
R14#sh ip bgp neighbors 85.10.22.1 received-routes
*Feb 16 08:03:01.165: %SYS-5-CONFIG_I: Configured from console by admin on console
R14#sh ip bgp neighbors 85.10.22.1 received-routes
BGP table version is 180, local router ID is 14.14.14.14
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *   0.0.0.0          85.10.22.1                             0 101 i

Total number of prefixes 1
```

***R14_IPv6***
```
R14#sh ip bgp ipv6 unicast neighbors 2000:0:1001:101::1 received-routes
BGP table version is 238, local router ID is 14.14.14.14
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *   ::/0             2000:0:1001:101::1
                                                              0 101 i

Total number of prefixes 1
```

### 4. Настроим провайдера Ламас так, чтобы в офис Москва отдавался только маршрут по умолчанию и префикс офиса С.-Петербург:

- На маршрутизаторе R21 разрешим трансляцию в офис Москва маршрута по-умолчанию и префиксов офиса С.-Петербург при помощи ***acess-list AS-Path***;
- Покажем конфигурацию маршрутизатора R21:

***R21***
```
R21#sh run | sec access-list
ip as-path access-list 1 permit _2042$

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

R21#sh run | sec bgp
router bgp 301
 bgp router-id 21.21.21.21
 bgp log-neighbor-changes
 neighbor 21.22.100.1 remote-as 101
 neighbor 24.100.40.1 remote-as 520
 neighbor 2000:0:301:101::1 remote-as 101
 neighbor 2000:0:520:301::1 remote-as 520
 neighbor 2000:0:1001:301::2 remote-as 1001
 neighbor 132.50.21.2 remote-as 1001
 !
 address-family ipv4
  network 21.22.100.0 mask 255.255.255.252
  network 24.100.40.0 mask 255.255.255.252
  network 132.50.21.0 mask 255.255.255.252
  neighbor 21.22.100.1 activate
  neighbor 24.100.40.1 activate
  no neighbor 2000:0:301:101::1 activate
  no neighbor 2000:0:520:301::1 activate
  no neighbor 2000:0:1001:301::2 activate
  neighbor 132.50.21.2 activate
  neighbor 132.50.21.2 default-originate
  neighbor 132.50.21.2 soft-reconfiguration inbound
  neighbor 132.50.21.2 filter-list 1 out
 exit-address-family
 !
 address-family ipv6
  network 2000:0:301:101::/112
  network 2000:0:520:301::/112
  network 2000:0:1001:301::/112
  neighbor 2000:0:301:101::1 activate
  neighbor 2000:0:520:301::1 activate
  neighbor 2000:0:1001:301::2 activate
  neighbor 2000:0:1001:301::2 default-originate
  neighbor 2000:0:1001:301::2 soft-reconfiguration inbound
  neighbor 2000:0:1001:301::2 filter-list 1 out
 exit-address-family
```

- Для проверки покажем таблицу приходящих префиксов на маршрутизаторе R15 от R21:

***R15_IPv4***
```
R15#sh ip bgp neighbor 132.50.21.1 received-routes
BGP table version is 88, local router ID is 15.15.15.15
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *   0.0.0.0          132.50.21.1                            0 301 i
 *   10.58.200.0/24   132.50.21.1                            0 301 520 2042 i
 *   10.64.20.0/30    132.50.21.1                            0 301 520 2042 i
 *   10.64.20.4/30    132.50.21.1                            0 301 520 2042 i
 *   10.64.20.8/30    132.50.21.1                            0 301 520 2042 i
 *   192.168.20.0     132.50.21.1                            0 301 520 2042 i

Total number of prefixes 6
```

***R15_IPv6***
```
R15#sh ip bgp ipv6 unicast neighbors 2000:0:1001:301::1 received-routes
BGP table version is 130, local router ID is 15.15.15.15
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *   ::/0             2000:0:1001:301::1
                                                              0 301 i
 *   FD00:0:16:18::/112
                       2000:0:1001:301::1
                                                              0 301 520 2042 i
 *   FD00:0:16:32::/112
                       2000:0:1001:301::1
                                                              0 301 520 2042 i
 *   FD00:0:17:18::/112
                       2000:0:1001:301::1
                                                              0 301 520 2042 i
 *   FD00:10:58:200::/64
                       2000:0:1001:301::1
                                                              0 301 520 2042 i
     Network          Next Hop            Metric LocPrf Weight Path
 *   FD00:192:168:20::/64
                       2000:0:1001:301::1
                                                              0 301 520 2042 i

Total number of prefixes 6
```

### 5. Проверим все сети в лабораторной работе на IP связность и задокументируем все изменения:

  - Проанонсируем все сети в протокол BGP на всех маршрутизаторах учавствующих в процессе BGP;
  - Добавим офисы Чокурдах и Лабытнанги в процесс BGP присвоив им номера AS и добавив интерфейс ***Loopback0*** на маршрутизаторах офисов для демонстрации IP-связности:
    * Чокурдах - *AS2222* (***Loopback0_IPv4 172.16.255.28/32***, ***Loopback0_IPv6 FD00:172:16:255::28/128***);
    * Лабытнанги - *AS1111* (***Loopback0_IPv4 172.16.255.27***, ***Loopback0_IPv6 FD00:172:16:255::27/128***).
   
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
B        2.2.2.0 [20/0] via 1.1.1.2, 06:28:12
      3.0.0.0/30 is subnetted, 1 subnets
B        3.3.3.0 [20/0] via 1.1.1.2, 06:28:12
      10.0.0.0/8 is variably subnetted, 16 subnets, 2 masks
B        10.58.10.0/24 [20/0] via 1.1.1.2, 06:28:12
B        10.58.100.0/24 [20/0] via 1.1.1.2, 00:27:46
B        10.58.200.0/24 [20/0] via 1.1.1.2, 00:10:09
B        10.64.20.0/30 [20/0] via 1.1.1.2, 00:11:10
B        10.64.20.4/30 [20/0] via 1.1.1.2, 00:10:40
B        10.64.20.8/30 [20/0] via 1.1.1.2, 00:10:40
B        10.64.52.0/30 [20/0] via 1.1.1.2, 05:44:48
B        10.64.52.4/30 [20/0] via 1.1.1.2, 06:06:35
B        10.64.52.8/30 [20/0] via 1.1.1.2, 06:06:04
B        10.64.52.12/30 [20/0] via 1.1.1.2, 05:36:59
B        10.64.100.0/30 [20/0] via 1.1.1.2, 00:27:46
B        10.64.100.4/30 [20/0] via 1.1.1.2, 00:27:46
B        10.64.100.8/30 [20/0] via 1.1.1.2, 00:27:46
B        10.64.100.12/30 [20/0] via 1.1.1.2, 00:27:46
B        10.64.100.16/30 [20/0] via 1.1.1.2, 00:27:46
B        10.64.100.20/30 [20/0] via 1.1.1.2, 00:27:46
      21.0.0.0/30 is subnetted, 1 subnets
B        21.22.100.0 [20/0] via 1.1.1.2, 06:28:12
      23.0.0.0/30 is subnetted, 1 subnets
B        23.100.40.0 [20/0] via 1.1.1.2, 06:28:12
      24.0.0.0/30 is subnetted, 2 subnets
B        24.100.40.0 [20/0] via 1.1.1.2, 06:28:12
B        24.100.40.4 [20/0] via 1.1.1.2, 06:28:12
      26.0.0.0/30 is subnetted, 1 subnets
B        26.100.40.0 [20/0] via 1.1.1.2, 06:28:12
      85.0.0.0/30 is subnetted, 1 subnets
B        85.10.22.0 [20/0] via 1.1.1.2, 06:28:12
      132.50.0.0/30 is subnetted, 1 subnets
B        132.50.21.0 [20/0] via 1.1.1.2, 06:28:12
      172.16.0.0/32 is subnetted, 8 subnets
B        172.16.255.14 [20/0] via 1.1.1.2, 00:27:46
B        172.16.255.15 [20/0] via 1.1.1.2, 00:27:46
B        172.16.255.23 [20/0] via 1.1.1.2, 05:20:10
B        172.16.255.24 [20/0] via 1.1.1.2, 05:22:57
B        172.16.255.25 [20/0] via 1.1.1.2, 05:18:20
B        172.16.255.26 [20/0] via 1.1.1.2, 05:24:11
B        172.16.255.28 [20/0] via 1.1.1.2, 06:28:12
B     192.168.10.0/24 [20/0] via 1.1.1.2, 00:27:46
B     192.168.20.0/24 [20/0] via 1.1.1.2, 00:10:09
B     192.168.100.0/24 [20/0] via 1.1.1.2, 06:28:12
```

***R27_IPv6***
```
R27#sh ipv6 rou bgp
IPv6 Routing Table - default - 39 entries
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
B   FD00:0:16:32::/112 [20/0]
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
B   FD00:192:168:20::/64 [20/0]
     via FE80::2, Ethernet0/0
B   FD00:192:168:100::/64 [20/0]
     via FE80::2, Ethernet0/0
  ```

Все изменения задокументированы [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_11/Configs)
