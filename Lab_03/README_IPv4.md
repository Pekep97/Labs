# DHCPv4

### Задание:

1. Создание сети и настройка основных параметров устройств;
  1.1 Настройка маршрутизации между VLAN на маршрутизаторе R1;
  1.2 Настройка активных интерфейсов и статической маршрутизации для обоих маршрутизаторов;
  1.3 Настройка VLAN и интерфейсов на SW1 и SW2;
2. Настройка и проверка двух серверов DHCPv4 на маршрутизаторе R1;
3. Настройка и проверка DHCP Relay на маршрутизаторе R2;
4. Задокументировать все изменения.

  ### Решение:

1. Создадим сеть и настроим основные параметры устройств;
  1.1 Настроим маршрутизацию между VLAN на маршрутизаторе R1;
  1.2 Настроим активные интерфейсы и статическую маршрутизацию для обоих маршрутизаторов;
  1.3 Настроим VLAN и интерфейсы на SW1 и SW2;
2. Настроим и проверим два сервера DHCPv4 на маршрутизаторе R1;
3. Настроим и проверим DHCP Relay на маршрутизаторе R2 и задокументируем все изменения.
   
  ### 1. Создадим сеть и настроим основные параметры устройств:

  Исследуемая схема:

  ![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_03/DHCPv4.png)
  

#### Таблица адресации:

| Device | Interface | IP Address   | Subnet Mask     | Default Gateway |
|--------|-----------|--------------|-----------------|-----------------|
| R1     | e0/1      | 10.0.0.1     | 255.255.255.252 | N/A             |
| R1     | e0/0      | N/A          | N/A             | N/A             |
| R1     | e0/1.100  | 192.168.1.1  | 255.255.255.192 | N/A             |
| R1     | e0/1.200  | 192.168.1.65 | 255.255.255.224 | N/A             |
| R1     | e0/1.1000 | N/A          | N/A             | N/A             |
| R2     | e0/1      | 10.0.0.2     | 255.255.255.252 | N/A             |
| R2     | e0/0      | 192.168.1.97 | 255.255.255.240 | N/A             |
| S1     | VLAN 200  | 192.168.1.66 | 255.255.255.224 | 192.168.1.65    |
| S2     | VLAN 1    | N/A          | N/A             | N/A             |
| PC-A   | NIC       | DHCP         | DHCP            | DHCP            |
| PC-B   | NIC       | DHCP         | DHCP            | DHCP            |

#### Таблица VLAN:

| VLAN | Name       | Interface Assigned |
|------|------------|--------------------|
| 1    | N/A        | S2: e0/0           |
| 100  | Clients    | S1: e0/0           |
| 200  | Management | S1: VLAN 200       |
| 1000 | Native     | N/A                |

На коммутаторах и роутерах настроим:
- время;
- зададим имя;
- назначим class в качестве зашифрованного пароля привилегированного режима;
- назначим cisco в качестве пароля консоли и включим вход;
- назначим cisco в качестве пароля VTY и включим вход;
	- зашифруем пароли в виде открытого текста.
- создадим баннер предупреждающий всех, что несанкционированный доступ запрещен.

Покажем для примера настройки на коммутаторе SW2:
```
conf t
!
clock timezone MSK3
!
hostname SW2
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
 end
```

### 1.1 Настроим маршрутизацию между VLAN на маршрутизаторе R1:

Настроим интерфейс е0/0:
- создадим подинтерфейсы использующие инкапсуляцию 802.1Q, и назначим IP-адреса из [таблицы:](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D0%B8)
- покажем результат.
```
R1#sh ip interface brief
Interface                  IP-Address      OK? Method Status                Prot                                                                                                                                                             ocol
Ethernet0/0                unassigned      YES unset  up                    up                                                                                                                                                               
Ethernet0/0.100            192.168.1.1     YES manual up                    up                                                                                                                                                               
Ethernet0/0.200            192.168.1.65    YES manual up                    up                                                                                                                                                               
Ethernet0/0.1000           unassigned      YES unset  up                    up                                                                                                                                                               
Ethernet0/1                unassigned      YES unset  administratively down down                                                                                                                                                             
Ethernet0/2                unassigned      YES unset  administratively down down                                                                                                                                                             
Ethernet0/3                unassigned      YES unset  administratively down down
```

### 1.2 Настроим активные интерфейсы и статическую маршрутизацию для обоих маршрутизаторов;
  
Настройки на R1
- присвоеним IP-адреса из [таблицы:](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D0%B8) на интерфейсе e0/1;
- настроим статический маршрут на R2;
- выведем результаты.

Покажем результат:
```
R1(config)#do sh ip route
S        192.168.1.96/28 [1/0] via 10.0.0.2

R1(config)#do sh ip inter brie
Interface                  IP-Address      OK? Method Status                Prot                                                                                                                                                             ocol
Ethernet0/0                unassigned      YES unset  up                    up                                                                                                                                                               
Ethernet0/0.100            192.168.1.1     YES manual up                    up                                                                                                                                                               
Ethernet0/0.200            192.168.1.65    YES manual up                    up                                                                                                                                                               
Ethernet0/0.1000           unassigned      YES unset  up                    up                                                                                                                                                               
Ethernet0/1                10.0.0.1        YES manual up                    up
```

Настройки на R2:
- присвоеним IP-адреса из [таблицы:](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D0%B8) на интерфейсах e0/0 и e0/1;
- настроим статический маршрут на R1;
- выведим результаты.

Покажем результат:
```
R2(config)#do sh ip inter brief
Interface                  IP-Address      OK? Method Status                Prot                                                                                                                                                             ocol
Ethernet0/0                unassigned      YES NVRAM  up                    up                                                                                                                                                               
Ethernet0/0.1              192.168.1.97    YES manual up                    up                                                                                                                                                               
Ethernet0/1                10.0.0.2        YES manual up                    up                                                                                                                                                               
Ethernet0/2                unassigned      YES NVRAM  administratively down down                                                                                                                                                             
Ethernet0/3                unassigned      YES NVRAM  administratively down down
```
``` R2#sh ip route

S        192.168.1.0/26 [1/0] via 10.0.0.1
S        192.168.1.64/27 [1/0] via 10.0.0.1
```

Продемонстрируем работу маршрутизации утилитой ping  на R2:
```
R2(config)#do ping 192.168.1.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms

R2(config)#do ping 192.168.1.65
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.65, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/4 ms
```
  
### 1.3 Настроим VLAN и интерфейсы на SW1 и SW2;

Сконфигурируем интерфейсы коммутаторов согласно [таблице](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-vlan) и покажем пример настройки на SW1
```
SW1#sh ip inter brief
Interface              IP-Address      OK? Method Status                Protocol
Ethernet0/0            unassigned      YES unset  up                    up
Ethernet0/1            unassigned      YES unset  up                    up
Ethernet0/2            unassigned      YES unset  up                    up
Ethernet0/3            unassigned      YES unset  up                    up
Vlan200                192.168.1.66    YES manual up                    up

SW1#sh vlan brief
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Et0/2, Et0/3
100  Clients                          active    Et0/0
200  Management                       active
1000 Native                           active
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
SW1#sh run inter e0/1
Building configuration...

Current configuration : 164 bytes
!
interface Ethernet0/1
 switchport trunk allowed vlan 100,200
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 1000
 switchport mode trunk
end

SW1#sh run inter e0/0
Building configuration...
Current configuration : 81 bytes
!
interface Ethernet0/0
 switchport access vlan 100
 switchport mode access
end
```

### 2. Настроим и проверим два сервера DHCPv4 на маршрутизаторе R1:

Настроим маршрутизатор R1 с пулами DHCPv4 для двух поддерживаемых подсетей. Ниже приведен только пул DHCP для подсети 192.168.1.0 255.255.255.192:
- исключим первые пять доступных адресов из каждого пула адресов;
- создадим пул DHCP (используем имя пула R1_Client_LAN);
- настроим доменное имя как ccna-lab.com;
- настроим соответствующий шлюз по умолчанию для каждого пула DHCP;
- настроим время аренды на 2 дня 12 часов 30 минут.
- затем настроим второй пул DHCPv4, используя имя пула R2_Client_LAN и рассчитанную сеть, маршрутизатор по умолчанию, и используем то же имя домена и время аренды, что и в предыдущем пуле DHCP.
- покажем результат;

ВЫведем ркзультат настройки DHCP пулов на R1:
```

