# Проектирование сети

### Задание:

1. Разработаете и задокументируете адресное пространство для лабораторного стенда.
2. Настроите ip адреса на каждом активном порту
3. Настроите каждый VPC в каждом офисе в своем VLAN.
4. Настроите VLAN/Loopbackup interface управления для сетевых устройств
5. Настроите сети офисов так, чтобы не возникало broadcast штормов, а использование линков было максимально оптимизировано

### Решение:

1. Разработаем и задокументируем адресное пространство для лабораторного стенда;
2. Настроим ip адреса на каждом активном порту;
3. Настроим каждый VPC в каждом офисе в своем VLAN;
4. Настроим VLAN/Loopbackup interface управления для сетевых устройств;
5. Настроим сети офисов так, чтобы не возникало broadcast штормов, а использование линков было максимально оптимизировано.

### 1. Разработаем и задокументируем адресное пространство для лабораторного стенда:

Опишем общий план действий:

- В Офисе Москва планируется собрать lacp между SW4 и SW5, настроить STP между SW2-SW5. Роутеры R12, R13 настроить VRRP, на котором будет висеть DHCP-сервер.
- В офисе С.-Петербург планируется два варианта организации L2 (Первый - просто собрать laсp между SW9 и SW10; Второй - объеденить их в стек, что было бы тоже интересным решением, но хотелось бы уточнить корректность работы этой технологии в eve-ng), на роутерах R16-R17 настроить VRRP, на котором будет висеть DHCP-сервер
- В офисе Чокурдах планируется организовать топологию "роутер на палочке", на R28 настроить DHCP-сервер.

### Исследуемая схема

![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_04/Lab_04.png)

### Таблица адрестного пространства (пока только IPv4):

|              |            |                 | Москва        |                     |             |               |            |                 |
| ------------ | ---------- | --------------- | ------------- | ------------------- | ----------- | ------------ | ----------- | -------------- |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R12          | e0/0.100   | MANAGEMENT_MSK  | 10.58.100.2   | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/0.10    | DHCP_MSK        | 192.168.10.2  | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/1.100   | MANAGEMENT_MSK  | 10.58.100.3   | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/1.10    | DHCP_MSK        | 192.168.10.3  | 255.255.255.0 (/24) |             |              |             |                |
| R13          | e0/0.100   | MANAGEMENT_MSK  | 10.58.100.4   | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/0.10    | DHCP_MSK        | 192.168.10.4  | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/1.100   | MANAGEMENT_MSK  | 10.58.100.5   | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/1.10    | DHCP_MSK        | 192.168.10.5  | 255.255.255.0 (/24) |             |              |             |                |
| VRRP_R12+R13 | \-         | MANAGEMENT_MSK  | 10.58.100.1   | 255.255.255.0 (/24) |             |              |             |                |
|              | \-         | DHCP_MSK        | 192.168.10.1  | 255.255.255.0 (/24) |             |              |             |                |
| SW2          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.12  | 255.255.255.0 (/24) | 10.58.100.1 |              |             |                |
| SW3          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.13  | 255.255.255.0 (/24) | 10.58.100.1 |              |             |                |
| SW4          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.14  | 255.255.255.0 (/24) | 10.58.100.1 |              |             |                |
| SW5          | VLAN100    | MANAGEMENT_MSK  | 10.58.100.15  | 255.255.255.0 (/24) | 10.58.100.1 |              |             |                |
| VPC1         | NIC        | \-              | DHCP          | DHCP                | DHCP        |              |             |                |
| VPC2         | NIC        | \-              | DHCP          | DHCP                | DHCP        |              |             |                |
|              |            |                 | С.-Петербург  |                     |             |              |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R16          | e0/0.200   | MANAGEMENT_SPB  | 10.58.200.2   | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/0.20    | DHCP_SPB        | 192.168.20.2  | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/2.200   | MANAGEMENT_SPB  | 10.58.200.3   | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/2.20    | DHCP_SPB        | 192.168.20.3  | 255.255.255.0 (/24) |             |              |             |                |
| R17          | e0/0.200   | MANAGEMENT_SPB  | 10.58.200.4   | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/0.20    | DHCP_SPB        | 192.168.20.4  | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/2.200   | MANAGEMENT_SPB  | 10.58.200.5   | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/2.20    | DHCP_SPB        | 192.168.20.5  | 255.255.255.0 (/24) |             |              |             |                |
| VRRP_R12+R13 | \-         | MANAGEMENT_SPB  | 10.58.200.1   | 255.255.255.0 (/24) |             |              |             |                |
|              | \-         | DHCP_SPB        | 192.168.20.1  | 255.255.255.0 (/24) |             |              |             |                |
| SW9          | VLAN200    | MANAGEMENT_SPB  | 10.58.200.109 | 255.255.255.0 (/24) | 10.58.200.1 |              |             |                |
| SW10         | VLAN200    | MANAGEMENT_SPB  | 10.58.200.110 | 255.255.255.0 (/24) | 10.58.200.1 |              |             |                |
| VPC          | NIC        | \-              | DHCP          | DHCP                | DHCP        |              |             |                |
| VPC8         | NIC        | \-              | DHCP          | DHCP                | DHCP        |              |             |                |
|              |            |                 | Чокурдах      |                     |             |              |             |                |
| Hostname     | Interfaces | Description     | IPv4-address  | Mask                | Gateway     | IPv6-address | IPv6-prefix | LLIPv6-address |
| R28          | e0/2.100   | MANAGEMENT_CHKR | 10.58.100.1   | 255.255.255.0 (/24) |             |              |             |                |
|              | e0/2.10    | DHCP_CHKR       | 192.168.10.1  | 255.255.255.0 (/24) |             |              |             |                |
| SW29         | VLAN100    | MANAGEMENT_CHKR | 10.58.100.129 | 255.255.255.0 (/24) | 10.58.100.1 |              |             |                |
| VPC30        | \-         | \-              | DHCP          | DHCP                | DHCP        |              |             |                |
| VPC31        | \-         | \-              | DHCP          | DHCP                | DHCP        |              |             |                |

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

