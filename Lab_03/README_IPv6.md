### DHCPv6

### Задание:

1. Создать сеть и настроить основные параметры устройств;
2. Проверить назначение адреса SLAAC от маршрутизатора R1;
3. Настроить и проверить сервер DHCPv6 без отслеживания состояния на маршрутизаторе R1;
4. Настроить и проверить сервер DHCPv6 с отслеживанием состояния на маршрутизаторе R1;
5. Настроить и проверить DHCPv6 Relay на маршрутизаторе R2.

### Решение:

1. Создадим сеть и настроим основные параметры устройств;
2. Проверим назначение адреса SLAAC от маршрутизатора R1;
3. Настроим и проверим сервер DHCPv6 без отслеживания состояния на маршрутизаторе R1;
4. Настроим и проверим сервер DHCPv6 с отслеживанием состояния на маршрутизаторе R1;
5. Настроим и проверим DHCPv6 Relay на маршрутизаторе R2 и задокументируем все изменения.

1. Создадим сеть и настроим основные параметры устройств:

Исследуемая схема:

!!!!!!!!!КАРТИНКА!!!!!!

### Таблица адресации:

| Device | Interface | IPv6 Address           |
| ------ | --------- | ---------------------- |
| R1     | e0/0      | 2001:db8:acad:2::1 /64 |
| R1     | e0/0      | fe80::1                |
| R1     | e0/1      | 2001:db8:acad:1::1/64  |
| R1     | e0/1      | fe80::1                |
| R2     | e0/0      | 2001:db8:acad:2::2/64  |
| R2     | e0/0      | fe80::2                |
| R2     | e0/1      | 2001:db8:acad:3::1 /64 |
| R2     | e0/1      | fe80::1                |
| PC-A   | NIC       | DHCP                   |
| PC-B   | NIC       | DHCP                   |

На роутерах настроим:
- время;
- зададим имя;
- назначим class в качестве зашифрованного пароля привилегированного режима;
- назначим cisco в качестве пароля консоли и включим вход;
- назначим cisco в качестве пароля VTY и включим вход;
	- зашифруем пароли в виде открытого текста.
- создадим баннер предупреждающий всех, что несанкционированный доступ запрещен.
- активируем IPv6 routing.

Покажем для примера настройки на роутера R1:
```
conf t
!
clock timezone MSK3
!
hostname R1
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
 end
```

Следом произведем следующие настройки:
- настроим интерфейсы е0/0 и е0/1 на маршрутизаторах R1 и R2 с адресами IPv6, указанными в [таблице](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv6.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D0%B8);
- настроим статическую маршрутизацию на R1 и R2;
- убедимся, что маршрутизация работает, пропинговав адрес е0/1 маршрутизатора R2 от маршрутизатора R1.

Результат настройки R1:
```
R1#sh ipv6 interface brief
Ethernet0/0            [up/up]
    FE80::1
    2001:DB8:ACAD:2::1
Ethernet0/1            [up/up]
    FE80::1
    2001:DB8:ACAD:1::1
Ethernet0/2            [administratively down/down]
    unassigned
Ethernet0/3            [administratively down/down]
    unassigned
!!!!!!!!!!!!!!!!!
R1#sh ipv6 route
IPv6 Routing Table - default - 6 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, HA - Home Agent, MR - Mobile Router, R - RIP
       H - NHRP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, NM - NEMO
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, la - LISP alt
       lr - LISP site-registrations, ld - LISP dyn-eid, a - Application
C   2001:DB8:ACAD:1::/64 [0/0]
     via Ethernet0/1, directly connected
L   2001:DB8:ACAD:1::1/128 [0/0]
     via Ethernet0/1, receive
C   2001:DB8:ACAD:2::/64 [0/0]
     via Ethernet0/0, directly connected
L   2001:DB8:ACAD:2::1/128 [0/0]
     via Ethernet0/0, receive
S   2001:DB8:ACAD:3::/64 [1/0]
     via 2001:DB8:ACAD:2::2
L   FF00::/8 [0/0]
     via Null0, receive
```

Результат настройки R2:
```
R2#sh ipv6 inter brief
Ethernet0/0            [up/up]
    FE80::2
    2001:DB8:ACAD:2::2
Ethernet0/1            [up/up]
    FE80::1
    2001:DB8:ACAD:3::1
Ethernet0/2            [administratively down/down]
    unassigned
Ethernet0/3            [administratively down/down]
!!!!!!!!!!!!!!!!!!!!!!!
R2#sh ipv6 route
IPv6 Routing Table - default - 6 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, HA - Home Agent, MR - Mobile Router, R - RIP
       H - NHRP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, NM - NEMO
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, la - LISP alt
       lr - LISP site-registrations, ld - LISP dyn-eid, a - Application
S   2001:DB8:ACAD:1::/64 [1/0]
     via 2001:DB8:ACAD:2::1
C   2001:DB8:ACAD:2::/64 [0/0]
     via Ethernet0/0, directly connected
L   2001:DB8:ACAD:2::2/128 [0/0]
     via Ethernet0/0, receive
C   2001:DB8:ACAD:3::/64 [0/0]
     via Ethernet0/1, directly connected
L   2001:DB8:ACAD:3::1/128 [0/0]
     via Ethernet0/1, receive
L   FF00::/8 [0/0]
     via Null0, receive
```

Убедимся, что маршрутизация работает, пропинговав адрес е0/1 маршрутизатора R2 от маршрутизатора R1:
```
R1#ping 2001:db8:acad:3::1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2001:DB8:ACAD:3::1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
```

### 2. Проверим назначение адреса SLAAC от маршрутизатора R1:

Убедимся, что VPC1 получает адрес IPv6, используя метод SLAAC, для этого включим его и подождав пару секунд проверим какой адрес он получил, должен получить 2001:db8:acad:1::/64
```
VPCS> sho

NAME   IP/MASK              GATEWAY                             GATEWAY
VPCS1  0.0.0.0/0            0.0.0.0
       fe80::250:79ff:fe66:680b/64
       2001:db8:acad:1:2050:79ff:fe66:680b/64 eui-64
```

Ответ на вопрос:

- Откуда взялась часть адреса, содержащая идентификатор хоста?
	- ОТВЕТ: при помощи алгоритма eui-64.

### 3. Настроим и проверим сервер DHCPv6 без отслеживания состояния на маршрутизаторе R1:

- Создадим пул DHCP IPv6 на маршрутизаторе R1 с именем R1-STATELESS. В составе этого пула назначим адрес DNS-сервера 2001:db8:acad::254 и имя домена — stateless.com, покажем результат настройки.
```
R1#sh ipv6 dhcp pool
DHCPv6 pool: R1-STATELESS
  DNS server: 2001:DB8:ACAD::254
  Domain name: STATELESS.com
  Active clients: 0
```

- Настроим интерфейс е0/1 на маршрутизаторе R1, чтобы предоставить флаг конфигурации OTHER для локальной сети маршрутизатора R1, и укажем только что созданный пул DHCP в качестве ресурса DHCP для этого интерфейса.
```
R1#sh run inter et0/1
Building configuration...

Current configuration : 184 bytes
!
interface Ethernet0/1
 no ip address
 ipv6 address FE80::1 link-local
 ipv6 address 2001:DB8:ACAD:1::1/64
 ipv6 enable
 ipv6 nd other-config-flag
 ipv6 dhcp server R1-STATELESS
end
```

### 4. Настроим и проверим сервер DHCPv6 с отслеживанием состояния на маршрутизаторе R1:

Создадим пул DHCPv6 на маршрутизаторе R1 для сети 2001:db8:acad:3:aaaa::/80. Это предоставит адреса локальной сети, подключенной к интерфейсу e0/1 на маршрутизаторе R2. В составе пула установим DNS-сервер 2001:db8:acad::254 и установите имя домена STATEFUL.com. Покажем результат:

```
R1#sh ipv6 dhcp pool
DHCPv6 pool: R1-STATELESS
  DNS server: 2001:DB8:ACAD::254
  Domain name: STATELESS.com
  Active clients: 0
DHCPv6 pool: R2-STATEFUL
  Address allocation prefix: 2001:DB8:ACAD:3:AAA::/80 valid 172800 preferred 86400 (0 in use, 0 conflicts)
  DNS server: 2001:DB8:ACAD::254
  Domain name: STATEFUL.com
  Active clients: 0
```

Назначим только что созданный пул DHCPv6 для интерфейса е0/0 на маршрутизаторе R1:
```
interface Ethernet0/0
 no ip address
 ipv6 address FE80::1 link-local
 ipv6 address 2001:DB8:ACAD:2::1/64
 ipv6 enable
 ipv6 dhcp server R2-STATEFUL
end
```

### 5. Настроим и проверим DHCPv6 Relay на маршрутизаторе R2 и задокументируем все изменения:

Поизведем настройку интерфейса е0/1 на R2  и покажем результат:
```
R2#sh run interface e0/1
Building configuration...

Current configuration : 215 bytes
!
interface Ethernet0/1
 no ip address
 ipv6 address FE80::1 link-local
 ipv6 address 2001:DB8:ACAD:3::1/64
 ipv6 enable
 ipv6 nd managed-config-flag
 ipv6 dhcp relay destination 2001:DB8:ACAD:2::1 Ethernet0/0
end
```

Все изменения приведены [сдесь.](https://github.com/Pekep97/Labs/tree/main/Lab_03/Configs)
