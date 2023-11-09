# Проектирование сети

### Задание:

1. Разработайте и задокументируете адресное пространство для лабораторного стенда;
2. Настройте ip адреса на каждом активном порту;
3. Настройте каждый VPC в каждом офисе в своем VLAN;
4. Настройте VLAN/Loopbackup interface управления для сетевых устройств;
5. Настройте сети офисов так, чтобы не возникало broadcast штормов, а использование линков было максимально оптимизировано;
6. Задокументируйте все изменения.

### Решение:

1. [Разработаем и задокументируем адресное пространство для лабораторного стенда;](https://github.com/Pekep97/Labs/tree/main/Lab_04#1-%D1%80%D0%B0%D0%B7%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%D0%B5%D0%BC-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%BD%D0%BE%D0%B5-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%BE-%D0%B4%D0%BB%D1%8F-%D0%BB%D0%B0%D0%B1%D0%BE%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BD%D0%BE%D0%B3%D0%BE-%D1%81%D1%82%D0%B5%D0%BD%D0%B4%D0%B0)
2. [Настроим ip адреса на каждом активном порту;](https://github.com/Pekep97/Labs/tree/main/Lab_04#2-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-ip-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0-%D0%BD%D0%B0-%D0%BA%D0%B0%D0%B6%D0%B4%D0%BE%D0%BC-%D0%B0%D0%BA%D1%82%D0%B8%D0%B2%D0%BD%D0%BE%D0%BC-%D0%BF%D0%BE%D1%80%D1%82%D1%83)
3. [Настроим каждый VPC в каждом офисе в своем VLAN;](https://github.com/Pekep97/Labs/tree/main/Lab_04#3-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BA%D0%B0%D0%B6%D0%B4%D1%8B%D0%B9-vpc-%D0%B2-%D0%BA%D0%B0%D0%B6%D0%B4%D0%BE%D0%BC-%D0%BE%D1%84%D0%B8%D1%81%D0%B5-%D0%B2-%D1%81%D0%B2%D0%BE%D0%B5%D0%BC-vlan)
4. [Настроим VLAN/Loopbackup interface управления для сетевых устройств;](https://github.com/Pekep97/Labs/tree/main/Lab_04#4-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-vlanloopbackup-interface-%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B4%D0%BB%D1%8F-%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D1%8B%D1%85-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2)
5. [Настроим сети офисов так, чтобы не возникало broadcast штормов, а использование линков было максимально оптимизировано и задокументируем все изменения.](https://github.com/Pekep97/Labs/tree/main/Lab_04#5-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D1%81%D0%B5%D1%82%D0%B8-%D0%BE%D1%84%D0%B8%D1%81%D0%BE%D0%B2-%D1%82%D0%B0%D0%BA-%D1%87%D1%82%D0%BE%D0%B1%D1%8B-%D0%BD%D0%B5-%D0%B2%D0%BE%D0%B7%D0%BD%D0%B8%D0%BA%D0%B0%D0%BB%D0%BE-broadcast-%D1%88%D1%82%D0%BE%D1%80%D0%BC%D0%BE%D0%B2-%D0%B0-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BB%D0%B8%D0%BD%D0%BA%D0%BE%D0%B2-%D0%B1%D1%8B%D0%BB%D0%BE-%D0%BC%D0%B0%D0%BA%D1%81%D0%B8%D0%BC%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE-%D0%BE%D0%BF%D1%82%D0%B8%D0%BC%D0%B8%D0%B7%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BE-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)

### 1. Разработаем и задокументируем адресное пространство для лабораторного стенда:

### Исследуемая схема

![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_04/Lab_04.png)

### Таблица адрестного пространства:

|              |            |                 | Москва        |                       |             |              |             |                |
|--------------|------------|-----------------|---------------|-----------------------|-------------|--------------|-------------|----------------|
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R12          | e0/0.100   | MANAGEMENT_MSK  | 10.58.100.2   | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/1.10    | DHCP_MSK        | 192.168.10.3  | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/2       | l3:to-R14       | 10.64.100.1   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/3       | l3:to-R15       | 10.64.100.5   | 255.255.255.252 (/30) |             |              |             |                |
| R13          | e0/0.100   | MANAGEMENT_MSK  | 10.58.100.4   | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/1.10    | DHCP_MSK        | 192.168.10.5  | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/2       | l3:to-R15       | 10.64.100.13  | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/3       | l3:to-R14       | 10.64.100.9   | 255.255.255.252 (/30) |             |              |             |                |
| VRRP_R12+R13 | -          | MANAGEMENT_MSK  | 10.58.100.1   | 255.255.255.0 (/24)   |             |              |             |                |
|              | -          | DHCP_MSK        | 192.168.10.1  | 255.255.255.0 (/24)   |             |              |             |                |
| R14          | e0/0       | l3:to-R12       | 10.64.100.2   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-R13       | 10.64.100.13  | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/2       | UPLINK          | 85.10.22.2    | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/3       | l3:to-R19       | 10.64.100.21  | 255.255.255.252 (/30) |             |              |             |                |
| R15          | e0/0       | l3:to-R13       | 10.64.100.14  | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-R12       | 10.64.100.6   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/2       | UPLINK          | 132.50.21.2   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/3       | l3:to-R20       | 10.64.100.17  | 255.255.255.252 (/30) |             |              |             |                |
| R19          | e0/0       | l3:to-R14       | 10.64.100.22  | 255.255.255.252 (/30) |             |              |             |                |
| R20          | e0/0       | l3:to-R15       | 10.64.100.18  | 255.255.255.252 (/30) |             |              |             |                |
| SW2          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.12  | 255.255.255.0 (/24)   | 10.58.100.1 |              |             |                |
| SW3          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.13  | 255.255.255.0 (/24)   | 10.58.100.1 |              |             |                |
| SW4          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.14  | 255.255.255.0 (/24)   | 10.58.100.1 |              |             |                |
| SW5          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.15  | 255.255.255.0 (/24)   | 10.58.100.1 |              |             |                |
| VPC1         | NIC        | -               | DHCP          | DHCP                  | DHCP        |              |             |                |
| VPC2         | NIC        | -               | DHCP          | DHCP                  | DHCP        |              |             |                |
|              |            |                 | Киторн        |                       |             |              |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R22          | e0/0       | l3:to-AS-1001   | 85.10.22.1    | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-AS-301    | 21.22.100.1   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/2       | l3:to-AS-520    | 23.100.40.2   | 255.255.255.252 (/30) |             |              |             |                |
|              |            |                 | Ламас         |                       |             |              |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R21          | e0/0       | l3:to-AS-1001   | 132.50.21.1   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-AS-101    | 21.22.100.2   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/2       | l3:to-AS-520    | 24.100.40.2   | 255.255.255.252 (/30) |             |              |             |                |
|              |            |                 | Триада        |                       |             |              |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R23          | e0/0       | l3:to-AS-101    | 23.100.40.1   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-R25       | 10.64.52.1    | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/2       | l3:to-R24       | 10.64.52.5    | 255.255.255.252 (/30) |             |              |             |                |
| R24          | e0/0       | l3:to-AS-301    | 24.100.40.1   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-R26       | 10.64.52.9    | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/2       | l3:to-R23       | 10.64.52.6    | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/3       | l3:to-AS-2042   | 24.100.40.5   | 255.255.255.252 (/30) |             |              |             |                |
| R25          | e0/0       | l3:to-R23       | 10.64.52.2    | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-LBTNG     | 1.1.1.2       | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/2       | l3:to-R26       | 10.64.52.13   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/3       | l3:to-CHKR      | 2.2.2.2       | 255.255.255.252 (/30) |             |              |             |                |
| R26          | e0/0       | l3:to-R24       | 10.64.52.10   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-CHKR      | 3.3.3.2       | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/2       | l3:to-R25       | 10.64.52.14   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/3       | l3:to-AS-2042   | 26.100.40.1   | 255.255.255.252 (/30) |             |              |             |                |
|              |            |                 | Лабытнанги    |                       |             |              |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R27          | e0/0       | l3:to-AS-520    | 1.1.1.1       | 255.255.255.252 (/30) |             |              |             |                |
|              |            |                 | С.-Петербург  |                       |             |              |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R16          | e0/0.200   | MANAGEMENT_SPB  | 10.58.200.2   | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/2.20    | DHCP_SPB        | 192.168.20.2  | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/1       | l3:to-R18       | 10.64.20.6    | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/3       | l3:to-R32       | 10.64.20.9    | 255.255.255.252 (/30) |             |              |             |                |
| R17          | e0/0.200   | MANAGEMENT_SPB  | 10.58.200.3   | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/2.20    | DHCP_SPB        | 192.168.20.3  | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/1       | l3:to-R18       | 10.64.20.2    | 255.255.255.252 (/30) |             |              |             |                |
| R18          | e0/0       | l3:to-R16       | 10.64.20.5    | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-R17       | 10.64.20.1    | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/2       | l3:to-R24       | 24.100.40.6   | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/3       | l3:to-R26       | 26.100.40.2   | 255.255.255.252 (/30) |             |              |             |                |
| R32          | e0/0       | l3:to-R16       | 10.64.20.10   | 255.255.255.252 (/30) |             |              |             |                |
| VRRP_R16+R17 | -          | MANAGEMENT_SPB  | 10.58.200.1   | 255.255.255.0 (/24)   |             |              |             |                |
|              | -          | DHCP_SPB        | 192.168.20.1  | 255.255.255.0 (/24)   |             |              |             |                |
| SW9          | VLAN200    | MANAGEMENT_SPB  | 10.58.200.109 | 255.255.255.0 (/24)   | 10.58.200.1 |              |             |                |
| SW10         | VLAN200    | MANAGEMENT_SPB  | 10.58.200.110 | 255.255.255.0 (/24)   | 10.58.200.1 |              |             |                |
| VPC          | NIC        | -               | DHCP          | DHCP                  | DHCP        |              |             |                |
| VPC8         | NIC        | -               | DHCP          | DHCP                  | DHCP        |              |             |                |
|              |            |                 | Чокурдах      |                       |             |              |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                  | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R28          | e0/2.100   | MANAGEMENT_CHKR | 10.58.10.1    | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/2.10    | DHCP_CHKR       | 192.168.100.1 | 255.255.255.0 (/24)   |             |              |             |                |
|              | e0/0       | l3:to-AS-520    | 3.3.3.1       | 255.255.255.252 (/30) |             |              |             |                |
|              | e0/1       | l3:to-AS-520    | 2.2.2.1       | 255.255.255.252 (/30) |             |              |             |                |
| SW29         | VLAN100    | MANAGEMENT_CHKR | 10.58.10.129  | 255.255.255.0 (/24)   | 10.58.10.1  |              |             |                |
| VPC30        | -          | -               | DHCP          | DHCP                  | DHCP        |              |             |                |
| VPC31        | -          | -               | DHCP          | DHCP                  | DHCP        |              |             |                |

### Таблица VLAN

| Офис         | VLAN-№ | VLAN-NAME       |
| ------------ | ------ | --------------- |
| Москва       | 10     | DHCP_MSK        |
|              | 100    | MANAGEMENT_MSK  |
| С.-Петербург | 20     | DHCP_SPB        |
|              | 200    | MANAGEMENT_SPB  |
| Чокурдах     | 10     | DHCP_CHKR       |
|              | 100    | MANAGEMENT_CHKR |

### 2. Настроим ip адреса на каждом активном порту:

На комутаторах и роутерах настроим:
- время;
- зададим имя;
- содадим пользователя admin с зашифрованным паролем admin;
- назначим class в качестве зашифрованного пароля привилегированного режима;
- назначим cisco в качестве пароля консоли и включим вход;
- назначим cisco в качестве пароля VTY и включим вход;
	- зашифруем пароли в виде открытого текста.
- создадим баннер предупреждающий всех, что несанкционированный доступ запрещен;
- назначим IP-адреса активным интерфейсам; 
- активируем IPv6 routing (на роутерах).

Покажем для примера настройки на роутера R12:
```
conf t
!
clock timezone MSK3
!
hostname R12
!
enable secret 5 $1$/yqZ$WE/0YR0XnODtDBsZeUD1j/
!
line con 0
 password cisco
 logging synchronous
 login local
 !
line vty 0 4
 password cisco
 login
 !
 banner $ unauthorized access prohibited $
 !
 username admin privilege 15 secret 5 $1$oiCq$/GWsWDICleh2G7ggNm8vm1
 !
 ipv6 unicast-routing
 !
R12#sh ip interface brief
Interface                  IP-Address      OK? Method Status                Protocol
Ethernet0/0                unassigned      YES unset  up                    up
Ethernet0/0.10             unassigned      YES manual deleted               down
Ethernet0/0.100            10.58.100.2     YES manual up                    up
Ethernet0/1                unassigned      YES unset  up                    up
Ethernet0/1.10             192.168.10.3    YES manual up                    up
Ethernet0/1.100            unassigned      YES manual up                    up
Ethernet0/2                unassigned      YES unset  administratively down down
Ethernet0/3                unassigned      YES unset  administratively down down
Ethernet1/0                unassigned      YES unset  administratively down down
Ethernet1/1                unassigned      YES unset  administratively down down
Ethernet1/2                unassigned      YES unset  administratively down down
Ethernet1/3                unassigned      YES unset  administratively down down
!
 end
```

### 3. Настроим каждый VPC в каждом офисе в своем VLAN:

Для выполнения этого пункта настроим порты коммутаторов к которым подключены VPC типа ***access***. Покажем настройку на SW2:

```
interface Ethernet0/2
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast edge
 spanning-tree bpdufilter enable
 spanning-tree bpduguard enable
 ip dhcp snooping trust
```

### 4. Настроим VLAN/Loopbackup interface управления для сетевых устройств:

На коммутаторах создадим интерфейс VLAN100, на роутерах создадимвиртуальные интерфейсы и зададим им адрес в соответствии с [таблицей.](https://github.com/Pekep97/Labs/blob/main/Lab_04/README.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D1%82%D0%BD%D0%BE%D0%B3%D0%BE-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%81%D1%82%D0%B2%D0%B0-%D0%BF%D0%BE%D0%BA%D0%B0-%D1%82%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE-ipv4)

Результат настройки покажем на SW2 и R12:

SW2
```
SW2#sh ip inter brief
Interface              IP-Address      OK? Method Status                Protocol
Ethernet0/0            unassigned      YES unset  up                    up
Ethernet0/1            unassigned      YES unset  up                    up
Ethernet0/2            unassigned      YES unset  up                    up
Ethernet0/3            unassigned      YES unset  up                    up
Vlan100                10.58.100.12    YES NVRAM  up                    up
```
R12
```
R12#sh ip inter brief
Interface                  IP-Address      OK? Method Status                Protocol
Ethernet0/0                unassigned      YES NVRAM  up                    up
Ethernet0/0.100            10.58.100.2     YES NVRAM  up                    up
Ethernet0/1                unassigned      YES NVRAM  up                    up
Ethernet0/1.10             192.168.10.3    YES NVRAM  up                    up
Ethernet0/1.100            unassigned      YES unset  up                    up
Ethernet0/2                unassigned      YES NVRAM  administratively down down
Ethernet0/3                unassigned      YES NVRAM  administratively down down
Ethernet1/0                unassigned      YES NVRAM  administratively down down
Ethernet1/1                unassigned      YES NVRAM  administratively down down
Ethernet1/2                unassigned      YES NVRAM  administratively down down
Ethernet1/3                unassigned      YES NVRAM  administratively down down
```

### 5. Настроим сети офисов так, чтобы не возникало broadcast штормов, а использование линков было максимально оптимизировано и задокументируем все изменения:

Опишем общий план действий:

- В Офисе Москва планируется собрать lacp между SW4 и SW5, настроить STP между SW2-SW5. Роутеры R12, R13 настроить VRRP, на котором будет висеть DHCP-сервер и шлюз по-умолчанию.
- В офисе С.-Петербург планируется собрать laсp между SW9 и SW10, на роутерах R16-R17 настроить VRRP, на котором будет висеть DHCP-сервер и шлюз по-умолчанию.
- В офисе Чокурдах планируется организовать топологию "роутер на палочке", на R28 настроить DHCP-сервер и шлюз по-умолчанию.

Покажем результат настройки на офисе Москва:

- покажем собранный lacp (lacp45) между SW4 и SW5 со стороны SW4:
```
SW4#show etherchannel 45 port-channel
                Port-channels in the group:
                ---------------------------

Port-channel: Po45    (Primary Aggregator)

------------

Age of the Port-channel   = 0d:00h:51m:00s
Logical slot/port   = 16/0          Number of ports = 2
HotStandBy port = null
Port state          = Port-channel Ag-Inuse
Protocol            =   LACP
Port security       = Disabled

Ports in the Port-channel:

Index   Load   Port     EC state        No of bits
------+------+------+------------------+-----------
  0     00     Et0/2    Passive            0
  0     00     Et0/3    Passive            0

Time since last port bundled:    0d:00h:50m:54s    Et0/2
```

- в результате настройки STP имеем следующие данные:
  	- Root Bridge - SW4;
  	- Alternative ports - SW3:Et0/1; SW2:Et0/0.

- покажем результат настройки VRRP на R12 и R13 на примере R12:
```
R12#sh vrrp brief
Interface          Grp Pri Time  Own Pre State   Master addr     Group addr
Et0/0.100          100 100 3609       Y  Backup  10.58.100.4     10.58.100.1
Et0/1.10           10  100 3609       Y  Backup  192.168.10.5    192.168.10.1
```

- Результат настройки DHCP-сервера:
	- на R12 создан DHCP-pool с именем DHCP_MSK_BACKUP и следующими параметрами:
```
ip dhcp excluded-address 192.168.10.1 192.168.10.127
ip dhcp pool DHCP_MSK_BACKUP
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 192.168.10.1
 domain-name DHCP_MSK.com
 lease 2 12 30
```

- на R13 создан DHCP-pool с именем DHCP_MSK и следующими параметрами:
 ```
R13#sh run | sec dhcp
ip dhcp excluded-address 192.168.10.1 192.168.10.5
ip dhcp excluded-address 192.168.10.128 192.168.10.255
ip dhcp pool DHCP_MSK
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 192.168.10.1
 domain-name DHCP_MSK.com
 lease 2 12 30
```

- покажем что VPC7 получил правильный адрес:
```
VPCS> sh ip

NAME        : VPCS[1]
IP/MASK     : 192.168.10.7/24
GATEWAY     : 192.168.10.1
DNS         : 192.168.10.1
DHCP SERVER : 192.168.10.5
DHCP LEASE  : 215348, 217800/108900/190575
DOMAIN NAME : DHCP_MSK.com
MAC         : 00:50:79:66:68:07
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:30000
MTU         : 1500
```

Такое разделение адресов сделано для удобства понимания, с какого физически роутера был получен адрес.

Все изменения приведены [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_04/Configs)
 
