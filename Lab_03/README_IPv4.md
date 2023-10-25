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

1. [Создадим сеть и настроим основные параметры устройств;](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#1-%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%B4%D0%B8%D0%BC-%D1%81%D0%B5%D1%82%D1%8C-%D0%B8-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2)
       1.1 [Настроим маршрутизацию между VLAN на маршрутизаторе R1;](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#11-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8E-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-vlan-%D0%BD%D0%B0-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80%D0%B5-r1)
	1.2 [Настроим активные интерфейсы и статическую маршрутизацию для обоих маршрутизаторов;](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#12-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%B0%D0%BA%D1%82%D0%B8%D0%B2%D0%BD%D1%8B%D0%B5-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81%D1%8B-%D0%B8-%D1%81%D1%82%D0%B0%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D1%83%D1%8E-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8E-%D0%B4%D0%BB%D1%8F-%D0%BE%D0%B1%D0%BE%D0%B8%D1%85-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2)
	1.3 [Настроим VLAN и интерфейсы на SW1 и SW2;](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#13-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-vlan-%D0%B8-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81%D1%8B-%D0%BD%D0%B0-sw1-%D0%B8-sw2)
2. [Настроим и проверим два сервера DHCPv4 на маршрутизаторе R1;](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#2-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%B8-%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%B8%D0%BC-%D0%B4%D0%B2%D0%B0-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B0-dhcpv4-%D0%BD%D0%B0-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80%D0%B5-r1)
3. [Настроим и проверим DHCP Relay на маршрутизаторе R2 и задокументируем все изменения.](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#3-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%B8-%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%B8%D0%BC-dhcp-relay-%D0%BD%D0%B0-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80%D0%B5-r2-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)
   
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
- присвоим IP-адреса из [таблицы:](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D0%B8) на интерфейсе e0/1;
- настроим статический маршрут на R2;
- выведем результаты.

Покажем результат:
```
R1(config)#do sh ip route
S        192.168.1.96/28 [1/0] via 10.0.0.2

R1(config)#do sh ip inter brie
Interface                  IP-Address      OK? Method Status                Protocol
Ethernet0/0                unassigned      YES unset  up                    up                                                                                                                                                               
Ethernet0/0.100            192.168.1.1     YES manual up                    up                                                                                                                                                               
Ethernet0/0.200            192.168.1.65    YES manual up                    up                                                                                                                                                               
Ethernet0/0.1000           unassigned      YES unset  up                    up                                                                                                                                                               
Ethernet0/1                10.0.0.1        YES manual up                    up
```

Настройки на R2:
- присвоим IP-адреса из [таблицы:](https://github.com/Pekep97/Labs/blob/main/Lab_03/README_IPv4.md#%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D0%B8) на интерфейсах e0/0 и e0/1;
- настроим статический маршрут на R1;
- выведим результаты.

Покажем результат:
```
R2(config)#do sh ip inter brief
Interface                  IP-Address      OK? Method Status                Protocol
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

Выведем ркзультат настройки DHCP пулов на R1:
```
ip dhcp excluded-address 192.168.1.1 192.168.1.5
ip dhcp excluded-address 192.168.1.97 192.168.1.101
!
ip dhcp pool R1_Client_LAN
 network 192.168.1.0 255.255.255.192
 domain-name ccna-lab.com
 dns-server 192.168.1.1
 default-router 192.168.1.1
 lease 2 12 30
!
ip dhcp pool R2_Client_LAN
 network 192.168.1.96 255.255.255.240
 domain-name ccna-lab.com
 dns-server 192.168.1.96
 default-router 192.168.1.96
 lease 2 12 30
```

Покажем что VPC1 получил IP-адрес по DHCP из пула R1_Client_LAN:
```
R1#sh ip dhcp binding
Bindings from all pools not associated with VRF:
IP address          Client-ID/              Lease expiration        Type
                    Hardware address/
                    User name
192.168.1.8         0100.5079.6668.05       Oct 27 2023 10:47 AM    Automatic
```

Покажем вывод команды ***show ip dhcp pool*** на R1:
```
R1#show ip dhcp pool

Pool R1_Client_LAN :
 Utilization mark (high/low)    : 100 / 0
 Subnet size (first/next)       : 0 / 0
 Total addresses                : 62
 Leased addresses               : 1
 Pending event                  : none
 1 subnet is currently in the pool :
 Current index        IP address range                    Leased addresses
 192.168.1.9          192.168.1.1      - 192.168.1.62      1

Pool R2_Client_LAN :
 Utilization mark (high/low)    : 100 / 0
 Subnet size (first/next)       : 0 / 0
 Total addresses                : 14
 Leased addresses               : 1
 Pending event                  : none
 1 subnet is currently in the pool :
 Current index        IP address range                    Leased addresses
 192.168.1.103        192.168.1.97     - 192.168.1.110     1
```

Покажем вывод команды ***show ip dhcp server statistics*** на R1:
```
R1# show ip dhcp server statistics
Memory usage         67277
Address pools        2
Database agents      0
Automatic bindings   2
Manual bindings      0
Expired bindings     0
Malformed messages   27
Secure arp entries   0

Message              Received
BOOTREQUEST          0
DHCPDISCOVER         50
DHCPREQUEST          4
DHCPDECLINE          0
DHCPRELEASE          0
DHCPINFORM           0

Message              Sent
BOOTREPLY            0
DHCPOFFER            4
DHCPACK              4
DHCPNAK              0
```

Покажем что порлучил VPC1:
```
VPCS> sh ip

NAME        : VPCS[1]
IP/MASK     : 192.168.1.8/26
GATEWAY     : 192.168.1.1
DNS         : 192.168.1.1
DHCP SERVER : 192.168.1.1
DHCP LEASE  : 169563, 217800/108900/190575
DOMAIN NAME : ccna-lab.com
MAC         : 00:50:79:66:68:05
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:30000
MTU         : 1500
```

### 3. Настроим и проверим DHCP Relay на маршрутизаторе R2 и задокументируем все изменения:

Для выполнения требований выполним следующее:
- Настроим на интерфейсе e0/0.1 роутера R2 ***ip helper-address*** и покажем его работу;
- Покжем вывод команды ***show ip dhcp binding*** на R1;
- Покжем вывод команды ***show ip dhcp server statistics*** на R1 и R2.

Настройка ***ip helper-address***:
```
R2#sh run inter e0/0.1
Building configuration...

Current configuration : 130 bytes
!
interface Ethernet0/0.1
 encapsulation dot1Q 1 native
 ip address 192.168.1.97 255.255.255.240
 ip helper-address 10.0.0.1
end
```

Покажем что VPC2 получает IP-адрес из пула R2_Client_LAN:
```
VPCS> sh ip

NAME        : VPCS[1]
IP/MASK     : 192.168.1.102/28
GATEWAY     : 192.168.1.96
DNS         : 192.168.1.96
DHCP SERVER : 10.0.0.1
DHCP LEASE  : 169461, 217800/108900/190575
DOMAIN NAME : ccna-lab.com
MAC         : 00:50:79:66:68:06
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:30000
MTU         : 1500
```

Вывод команды ***show ip dhcp binding*** на R1:
```
R1#show ip dhcp binding
Bindings from all pools not associated with VRF:
IP address          Client-ID/              Lease expiration        Type
                    Hardware address/
                    User name
192.168.1.8         0100.5079.6668.05       Oct 27 2023 10:47 AM    Automatic
192.168.1.102       0100.5079.6668.06       Oct 27 2023 10:56 AM    Automatic
```

Dывод команды ***show ip dhcp server statistics*** на R1 и R2:
```
R1#show ip dhcp server statistics
Memory usage         67277
Address pools        2
Database agents      0
Automatic bindings   2
Manual bindings      0
Expired bindings     0
Malformed messages   27
Secure arp entries   0

Message              Received
BOOTREQUEST          0
DHCPDISCOVER         50
DHCPREQUEST          4
DHCPDECLINE          0
DHCPRELEASE          0
DHCPINFORM           0

Message              Sent
BOOTREPLY            0
DHCPOFFER            4
DHCPACK              4
DHCPNAK              0
```
```
R2#sh ip dhcp server statistics
Memory usage         22565
Address pools        0
Database agents      0
Automatic bindings   0
Manual bindings      0
Expired bindings     0
Malformed messages   0
Secure arp entries   0

Message              Received
BOOTREQUEST          0
DHCPDISCOVER         0
DHCPREQUEST          0
DHCPDECLINE          0
DHCPRELEASE          0
DHCPINFORM           0

Message              Sent
BOOTREPLY            0
DHCPOFFER            0
DHCPACK              0
DHCPNAK              0
```

Все изменения приведены [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_03/Configs)
