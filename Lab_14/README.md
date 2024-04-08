# IPSec over DmVPN

### Задание: 

1. Настроить GRE поверх IPSec между офисами Москва и С.-Петербург;
2. Настроить DMVPN поверх IPSec между офисами Москва и Чокурдах, Лабытнанги.

### Решение:

1. [Настроим GRE поверх IPSec между офисами Москва и С.-Петербург;](https://github.com/Pekep97/Labs/tree/main/Lab_14#1-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-gre-%D0%BF%D0%BE%D0%B2%D0%B5%D1%80%D1%85-ipsec-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-%D0%BE%D1%84%D0%B8%D1%81%D0%B0%D0%BC%D0%B8-%D0%BC%D0%BE%D1%81%D0%BA%D0%B2%D0%B0-%D0%B8-%D1%81-%D0%BF%D0%B5%D1%82%D0%B5%D1%80%D0%B1%D1%83%D1%80%D0%B3)
2. [Настроим DMVPN поверх IPSec между Москва и Чокурдах, Лабытнанги и задокументируем все изменения;](https://github.com/Pekep97/Labs/tree/main/Lab_14#2-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-dmvpn-%D0%BF%D0%BE%D0%B2%D0%B5%D1%80%D1%85-ipsec-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-%D0%BC%D0%BE%D1%81%D0%BA%D0%B2%D0%B0-%D0%B8-%D1%87%D0%BE%D0%BA%D1%83%D1%80%D0%B4%D0%B0%D1%85-%D0%BB%D0%B0%D0%B1%D1%8B%D1%82%D0%BD%D0%B0%D0%BD%D0%B3%D0%B8-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)
Дополнительно: Для IPSec используются CA и сертификаты.

### 1. Настроим GRE поверх IPSec между офисами Москва и С.-Петербург:

![Исходная схема](https://github.com/Pekep97/Labs/blob/main/Lab_14/Lab_14.png)

### 
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
|              | Tunnel0  | -               | 10.0.0.1   | 255.255.255.0(/24)  | -           |   |         |         |
|              | Tunnel1  | -               | 10.0.1.1   | 255.255.255.0(/24)  | -           |   |         |         |
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
|              | Tunnel1  | -               | 10.0.1.2   | 255.255.255.0(/24)  | -           |   |         |         |
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
|              | Tunnel0  | -               | 10.0.0.2   | 255.255.255.0(/24)  | -           |   |         |         |
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
|              | Tunnel1  | -               | 10.0.1.3   | 255.255.255.0(/24)  | -           |   |         |         |
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

- Настроим центр сертификации на R15:

```
ip domain name otus.ru
ip http server
crypto key generate rsa general-keys label CA exportable modulus 2048
crypto pki server CA
 database level complete
 no shut
```

- На маршрутизаторах R15, R18, R27, R28 создадим ключи и отправим запрос на подпись сертификатов на CA. Покажем на R18:

***R18***
```
R18#sh run | sec pki
crypto pki trustpoint VPN
 enrollment url http://10.0.0.1:80
 ip-address Tunnel0
 revocation-check none
crypto pki certificate chain VPN
 certificate 06
  3082023A 30820122 A0030201 02020106 300D0609 2A864886 F70D0101 05050030
  0D310B30 09060355 04031302 4341301E 170D3234 30343038 30373130 35345A17
  0D323530 34303830 37313035 345A302B 31293010 06092A86 4886F70D 01090216
  03523138 30150609 2A864886 F70D0109 08130831 302E302E 302E3230 5C300D06
  092A8648 86F70D01 01010500 034B0030 48024100 B69E6954 EF4DF549 9F22CD76
  81DEB4A3 FD3AC5F6 7B1581AB 60FC0C2A 70808EA3 66D3AB34 47908D31 D91EE66E
  DF869BF5 FD68C891 2D3AA045 3DF5DC65 68EF5BE9 02030100 01A34F30 4D300B06
  03551D0F 04040302 05A0301F 0603551D 23041830 16801407 601554DB 36CA5A76
  EC7BFEF1 104C18F4 8FD2F530 1D060355 1D0E0416 0414CF1A 3B1FAF1D DCFA1D7D
  7934D5A7 898AC1A2 53DF300D 06092A86 4886F70D 01010505 00038201 0100C307
  2D742466 957D0F4B B11BD142 52C286E7 8496FD73 4ED586DA AF21DD8F 13550586
  FB013BB0 24C118CE 7D4E7D8A C2611687 7FD149AB DF06DBEA 44B0CF5A 202246A4
  277B290F ABA71BDE 090ED8A2 F15BF9F7 39734B73 12732719 E1F873CA 8AAD31E7
  608012C0 834A20FA 7067810B A3313404 21FC9362 3ECFBB1F 0601124D 2B4842D3
  94951949 E573BACC 45FC7D5B 6953FFF7 B93BF1A4 409FA239 D051726C 8C1982F7
  6188EF8B 70FC7A29 D3648EF9 F4C196AC 81685B6F FD70222A 005F2B61 3612100E
  9CF1E76A F025B27C 7A90C572 9D48475C AD1F3623 3A0D3EB3 BD07523A 88A6A9D3
  1F373638 2D92A879 DA58865C A9FEC1B1 D707756C D20D413E 45281813 BED3
        quit
 certificate ca 01
  308202F8 308201E0 A0030201 02020101 300D0609 2A864886 F70D0101 04050030
  0D310B30 09060355 04031302 4341301E 170D3234 30343032 31363437 34305A17
  0D323730 34303231 36343734 305A300D 310B3009 06035504 03130243 41308201
  22300D06 092A8648 86F70D01 01010500 0382010F 00308201 0A028201 0100E3CC
  B7F6B7D0 42275FE9 556BF584 5D102FAD 62AF1826 CE1EC77B ABB45620 558664BC
  25B5FA3A 440A5BA7 C906FFC8 D9494289 F16B1510 B292710B 50454731 B260F9DE
  843D5FE9 112D6051 93E46A26 C652729F 0E933885 CC17EB17 3DC398C1 2D8FDCCC
  D149D1B8 4815BCCC E80E8AB7 275AF173 6598A8C4 291897ED D5D04BF9 E1B6DF11
  09F32903 D892F4F8 FC2EBBE3 76BA2D46 1663F061 79277896 24F7A921 EEFD8F05
  BE62BEAC 6649D52E 7A540A63 2B9A5C78 0354F6B6 2F377511 C71A43C8 F45C796B
  AA5BF4F4 0C7AA102 0EDCC681 F352D815 AD1172B9 0653F0A7 FF28C03C C662E1C9
  6751392A B64DD072 3D78D234 EF36C02F EA18066D 25E2F9F7 E03A291E F6030203
  010001A3 63306130 0F060355 1D130101 FF040530 030101FF 300E0603 551D0F01
  01FF0404 03020186 301F0603 551D2304 18301680 14076015 54DB36CA 5A76EC7B
  FEF1104C 18F48FD2 F5301D06 03551D0E 04160414 07601554 DB36CA5A 76EC7BFE
  F1104C18 F48FD2F5 300D0609 2A864886 F70D0101 04050003 82010100 36D39310
  4F98EA90 809C0204 3489D8C4 70E3AFCF A03013D4 B96F2794 C7918827 C1755F88
  2B71A7E1 360EE89A 8038F256 72BF5C51 CF0F8933 909B5CAD 4FAF1A7C B537B030
  2CFC8598 E6402DF3 C0E85840 B926873D 59E5339C ED292823 C22CDA79 D6CFE7C8
  2E3B7148 6E992638 C85CCDE1 08C72742 D88A14F1 7DC02779 675DC3D7 3A229BF3
  84D97ECD 10F6CCA2 C5733487 4A68F5E5 1F9139CA 0EDBF76D 95834B50 5CC57670
  714CF87B 95EEB37D B09E25C0 32BDC0F9 2458F961 D356CF7A 5654AAE2 01716238
  3CB05668 60CD124E 84B5592C AF5341A9 F7486778 737F9A2D 2980BFA8 1CADE1A0
  C1A9D106 C53FA3A6 7790A814 860EE63F 848E50F9 61CDF846 8809F6C4
        quit
```

- Настроим первую фазу (IKEv2) на R15 и R18. Покажем настройку на R18 (R15 по аналогии):

***R18***
```
R18#sh run | sec ikev2
crypto ikev2 proposal PROP_R15
 encryption aes-cbc-128
 integrity md5
 group 2
crypto ikev2 policy IKEV2
 proposal PROP_R15
crypto ikev2 profile PROFILE1
 match address local interface Loopback1
 match identity remote address 0.0.0.0
 authentication remote rsa-sig
 authentication local rsa-sig
 pki trustpoint VPN
 set ikev2-profile PROFILE1
```

- Настроим IPSEC на R15 и R18. Покажем настройку на R18 (R15 по аналогии):

***R18***
```
R18#sh run | sec ipsec
crypto ipsec transform-set IPSEC_TS esp-aes esp-md5-hmac
 mode tunnel
crypto ipsec profile IPSEC_PROF
 set transform-set IPSEC_TS
 set ikev2-profile PROFILE1
 tunnel protection ipsec profile IPSEC_PROF
```

- Добавим к туннельным интерфейсам ***Tunnel0*** привязку к IPSEC-у:

```
R18#sh run int t0
Building configuration...

Current configuration : 161 bytes
!
interface Tunnel0
 ip address 10.0.0.2 255.255.255.0
 tunnel source Loopback1
 tunnel destination 37.85.13.15
 !!!!!! tunnel protection ipsec profile IPSEC_PROF !!!!!!!!!!
end
```

- Проверим установление фаз на R18:

***IKEv2_R18***
```
R18#sh crypto ikev2 sa
 IPv4 Crypto IKEv2  SA

Tunnel-id Local                 Remote                fvrf/ivrf            Status
1         53.17.29.18/500       37.85.13.15/500       none/none            READY
      Encr: AES-CBC, keysize: 128, PRF: MD5, Hash: MD596, DH Grp:2, Auth sign: RSA, Auth verify: RSA
      Life/Active Time: 86400/7762 sec

 IPv6 Crypto IKEv2  SA
```

***IPSEC_R18***
```
R18#sh crypto ipsec sa

interface: Tunnel0
    Crypto map tag: Tunnel0-head-0, local addr 53.17.29.18

   protected vrf: (none)
   local  ident (addr/mask/prot/port): (53.17.29.18/255.255.255.255/47/0)
   remote ident (addr/mask/prot/port): (37.85.13.15/255.255.255.255/47/0)
   current_peer 37.85.13.15 port 500
     PERMIT, flags={origin_is_acl,}
    #pkts encaps: 851, #pkts encrypt: 851, #pkts digest: 851
    #pkts decaps: 851, #pkts decrypt: 851, #pkts verify: 851
    #pkts compressed: 0, #pkts decompressed: 0
    #pkts not compressed: 0, #pkts compr. failed: 0
    #pkts not decompressed: 0, #pkts decompress failed: 0
    #send errors 0, #recv errors 0

     local crypto endpt.: 53.17.29.18, remote crypto endpt.: 37.85.13.15
     plaintext mtu 1438, path mtu 1500, ip mtu 1500, ip mtu idb Ethernet0/2
     current outbound spi: 0x7573FF1(123158513)
     PFS (Y/N): N, DH group: none

     inbound esp sas:
      spi: 0x59479A40(1497864768)
        transform: esp-aes esp-md5-hmac ,
        in use settings ={Tunnel, }
        conn id: 10, flow_id: SW:10, sibling_flags 80000040, crypto map: Tunnel0-head-0
        sa timing: remaining key lifetime (k/sec): (4337195/2713)
        IV size: 16 bytes
        replay detection support: Y
        Status: ACTIVE(ACTIVE)

     inbound ah sas:

     inbound pcp sas:

     outbound esp sas:
      spi: 0x7573FF1(123158513)
        transform: esp-aes esp-md5-hmac ,
        in use settings ={Tunnel, }
        conn id: 9, flow_id: SW:9, sibling_flags 80000040, crypto map: Tunnel0-head-0
        sa timing: remaining key lifetime (k/sec): (4337195/2713)
        IV size: 16 bytes
        replay detection support: Y
        Status: ACTIVE(ACTIVE)

     outbound ah sas:

     outbound pcp sas:
```

- Покажем что туннель в работе продемонстрировав таблицу маршрутизации ***OSPF*** на R18, который работает через туннель:

```
R18#sh ip rou ospf
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       a - application route
       + - replicated route, % - next hop override

Gateway of last resort is 0.0.0.0 to network 0.0.0.0

      10.0.0.0/8 is variably subnetted, 19 subnets, 3 masks
O IA     10.0.1.0/24 [110/2000] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.58.100.0/30 [110/1020] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.58.100.4/30 [110/1020] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.64.100.0/30 [110/1020] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.64.100.4/30 [110/1010] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.64.100.8/30 [110/1020] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.64.100.12/30 [110/1010] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.64.100.16/30 [110/1010] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.64.100.20/30 [110/1020] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.64.100.24/30 [110/1010] via 10.0.0.1, 02:13:25, Tunnel0
O IA     10.64.100.28/30 [110/1020] via 10.0.0.1, 02:13:25, Tunnel0
      172.16.0.0/32 is subnetted, 8 subnets
O IA     172.16.255.12 [110/1011] via 10.0.0.1, 02:13:25, Tunnel0
O IA     172.16.255.13 [110/1011] via 10.0.0.1, 02:13:25, Tunnel0
O IA     172.16.255.14 [110/1011] via 10.0.0.1, 02:13:25, Tunnel0
O IA     172.16.255.15 [110/1001] via 10.0.0.1, 02:13:25, Tunnel0
O IA     172.16.255.19 [110/1021] via 10.0.0.1, 02:13:25, Tunnel0
O IA     172.16.255.20 [110/1011] via 10.0.0.1, 02:13:25, Tunnel0
```

### 2. Настроим DMVPN поверх IPSec между Москва и Чокурдах, Лабытнанги и задокументируем все изменения:

- На R15 создадим еще один ***profile IPSEC*** :

***R15***
```
crypto ipsec transform-set DMVPN esp-aes esp-md5-hmac
 mode transport
crypto ipsec profile DMVPN_PROF
 set transform-set DMVPN
 set ikev2-profile PROFILE1
 ```

- На R27 и R28 настроим ***IKEv2*** и ***IPSEC***. Покажем настройку ***R27***

***IKEv2_R27***
```
crypto ikev2 proposal PROP_R15
 encryption aes-cbc-128
 integrity md5
 group 2
crypto ikev2 policy IKEV2
 proposal PROP_R15
crypto ikev2 profile PROFILE1
 match address local interface Loopback1
 match identity remote address 0.0.0.0
 authentication remote rsa-sig
 authentication local rsa-sig
 pki trustpoint VPN
```

***IPSEC_R27***
```
crypto ipsec transform-set DMVPN esp-aes esp-md5-hmac
 mode transport
crypto ipsec profile DMVPN_PROF
 set transform-set DMVPN
 set ikev2-profile PROFILE1
```

- Добавим к туннельномым интерфейсам ***Tunnel1*** привязку к IPSEC-у:

```
R15#sh run int t1
Building configuration...

Current configuration : 313 bytes
!
interface Tunnel1
 ip address 10.0.1.1 255.255.255.0
 no ip redirects
 ip mtu 1400
 ip nhrp map multicast dynamic
 ip nhrp network-id 1
 ip tcp adjust-mss 1360
 ip ospf network broadcast
 ip ospf priority 255
 tunnel source Loopback1
 tunnel mode gre multipoint
 !!!!!!! tunnel protection ipsec profile DMVPN_PROF !!!!!!!!!!
end
```

- Проверим установление фаз на R27:

***IKEv2_R27***
```
R27#sh crypto ikev2 sa
 IPv4 Crypto IKEv2  SA

Tunnel-id Local                 Remote                fvrf/ivrf            Status
1         115.237.93.27/500     37.85.13.15/500       none/none            READY
      Encr: AES-CBC, keysize: 128, PRF: MD5, Hash: MD596, DH Grp:2, Auth sign: RSA, Auth verify: RSA
      Life/Active Time: 86400/10937 sec

 IPv6 Crypto IKEv2  SA
```

***IPSEC_R27***
```
R27#sh crypto ipsec sa

interface: Tunnel1
    Crypto map tag: Tunnel1-head-0, local addr 115.237.93.27

   protected vrf: (none)
   local  ident (addr/mask/prot/port): (115.237.93.27/255.255.255.255/47/0)
   remote ident (addr/mask/prot/port): (37.85.13.15/255.255.255.255/47/0)
   current_peer 37.85.13.15 port 500
     PERMIT, flags={origin_is_acl,}
    #pkts encaps: 1223, #pkts encrypt: 1223, #pkts digest: 1223
    #pkts decaps: 1249, #pkts decrypt: 1249, #pkts verify: 1249
    #pkts compressed: 0, #pkts decompressed: 0
    #pkts not compressed: 0, #pkts compr. failed: 0
    #pkts not decompressed: 0, #pkts decompress failed: 0
    #send errors 0, #recv errors 0

     local crypto endpt.: 115.237.93.27, remote crypto endpt.: 37.85.13.15
     plaintext mtu 1458, path mtu 1500, ip mtu 1500, ip mtu idb (none)
     current outbound spi: 0x87EE7282(2280551042)
     PFS (Y/N): N, DH group: none

     inbound esp sas:
      spi: 0xC428E906(3291015430)
        transform: esp-aes esp-md5-hmac ,
        in use settings ={Transport, }
        conn id: 7, flow_id: SW:7, sibling_flags 80000000, crypto map: Tunnel1-head-0
        sa timing: remaining key lifetime (k/sec): (4215818/2970)
        IV size: 16 bytes
        replay detection support: Y
        Status: ACTIVE(ACTIVE)

     inbound ah sas:

     inbound pcp sas:

     outbound esp sas:
      spi: 0x87EE7282(2280551042)
        transform: esp-aes esp-md5-hmac ,
        in use settings ={Transport, }
        conn id: 8, flow_id: SW:8, sibling_flags 80000000, crypto map: Tunnel1-head-0
        sa timing: remaining key lifetime (k/sec): (4215818/2970)
        IV size: 16 bytes
        replay detection support: Y
        Status: ACTIVE(ACTIVE)

     outbound ah sas:

     outbound pcp sas:
```

- Покажем что туннель в работе продемонстрировав таблицу маршрутизации ***OSPF*** на R27, который работает через туннель:

```
R27#sh ip rou ospf
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       a - application route
       + - replicated route, % - next hop override

Gateway of last resort is 1.1.1.2 to network 0.0.0.0

      10.0.0.0/8 is variably subnetted, 16 subnets, 3 masks
O IA     10.0.0.0/24 [110/2000] via 10.0.1.1, 02:45:03, Tunnel1
O IA     10.58.100.0/30 [110/1020] via 10.0.1.1, 03:03:44, Tunnel1
O IA     10.58.100.4/30 [110/1020] via 10.0.1.1, 03:03:44, Tunnel1
O E2     10.58.200.0/24 [110/20] via 10.0.1.1, 02:44:48, Tunnel1
O E2     10.64.20.0/30 [110/20] via 10.0.1.1, 02:44:48, Tunnel1
O IA     10.64.100.0/30 [110/1020] via 10.0.1.1, 03:03:44, Tunnel1
O IA     10.64.100.4/30 [110/1010] via 10.0.1.1, 03:03:44, Tunnel1
O IA     10.64.100.8/30 [110/1020] via 10.0.1.1, 03:03:44, Tunnel1
O IA     10.64.100.12/30 [110/1010] via 10.0.1.1, 03:03:44, Tunnel1
O IA     10.64.100.16/30 [110/1010] via 10.0.1.1, 03:03:44, Tunnel1
O IA     10.64.100.20/30 [110/1020] via 10.0.1.1, 03:03:44, Tunnel1
O IA     10.64.100.24/30 [110/1010] via 10.0.1.1, 03:03:44, Tunnel1
O IA     10.64.100.28/30 [110/1020] via 10.0.1.1, 03:03:44, Tunnel1
      172.16.0.0/32 is subnetted, 8 subnets
O IA     172.16.255.12 [110/1011] via 10.0.1.1, 03:03:44, Tunnel1
O IA     172.16.255.13 [110/1011] via 10.0.1.1, 03:03:44, Tunnel1
O IA     172.16.255.14 [110/1011] via 10.0.1.1, 03:03:44, Tunnel1
O IA     172.16.255.15 [110/1001] via 10.0.1.1, 03:03:44, Tunnel1
O IA     172.16.255.19 [110/1021] via 10.0.1.1, 03:03:44, Tunnel1
O IA     172.16.255.20 [110/1011] via 10.0.1.1, 03:03:44, Tunnel1
O E2  192.168.20.0/24 [110/20] via 10.0.1.1, 02:44:48, Tunnel1
```

- Все изменения задокументированны [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_14/Configs)
