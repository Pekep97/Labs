# VLAN IPv4

### Задание:

1. Создание сети и настройка основных параметров устройств;
2. Создание сетей VLAN и назначение портов коммутатора;
3. Настройка транка 802.1Q между коммутаторами;
4. Настройка маршрутизации между VLAN на маршрутизаторе;
5. Проверка того, что маршрутизация между VLAN работает;
6. Задокументировать все изменения.

### Решение:

1. [Создадим сети и настроим основные параметры устройств;](https://github.com/Pekep97/Labs/blob/main/Lab_01/README.md#1-%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%B4%D0%B8%D0%BC-%D1%81%D0%B5%D1%82%D0%B8-%D0%B8-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2)
2. [Создадим сети VLAN и назначим их на порты коммутаторов;](https://github.com/Pekep97/Labs/blob/main/Lab_01/README.md#2-%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%B4%D0%B8%D0%BC-%D1%81%D0%B5%D1%82%D0%B8-vlan-%D0%B8-%D0%BD%D0%B0%D0%B7%D0%BD%D0%B0%D1%87%D0%B8%D0%BC-%D0%B8%D1%85-%D0%BD%D0%B0-%D0%BF%D0%BE%D1%80%D1%82%D1%8B-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%BE%D0%B2)
3. [Настроим транк 802.1Q между коммутаторами;](https://github.com/Pekep97/Labs/blob/main/Lab_01/README.md#3-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D1%82%D1%80%D0%B0%D0%BD%D0%BA-8021q-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%B0%D0%BC%D0%B8)
4. [Настроим маршрутизацию между VLAN на маршрутизаторе;](https://github.com/Pekep97/Labs/blob/main/Lab_01/README.md#4-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8E-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-vlan-%D0%BD%D0%B0-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80%D0%B5)
5. [Проверим что маршрутизация между VLAN работает и задокументируем все изменения.](https://github.com/Pekep97/Labs/blob/main/Lab_01/README.md#5-%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%B8%D0%BC-%D1%87%D1%82%D0%BE-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-vlan-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%D0%B5%D1%82-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%B8%D1%8F)

### 1. Создадим сети и настроим основные параметры устройств:

Общая таблица сетей:
| Device | Interface | IPv4 adress  | Subnet mask IPv4 | Default Gateway IPv4 | Link-Local IPv6 adress |
|--------|-----------|--------------|------------------|----------------------|------------------------|
| R1     | e0/0.3    | 192.168.3.1  | 255.255.255.0    | N/A                  | fe80::1                |
|        | e0/0.4    | 192.168.4.1  | 255.255.255.0    |                      |                        |
|        | e0/0.8    | N/A          |                  |                      |                        |
| SW1    | VLAN 3    | 192.168.3.11 | 255.255.255.0    | 192.168.3.1          | fe80::11               |
| SW2    | VLAN 3    | 192.168.3.12 | 255.255.255.0    | 192.168.3.1          | fe80::12               |
| PC-1   | NIC       | 192.168.3.3  | 255.255.255.0    | 192.168.3.1          |                        |
| PC-2   | NIC       | 192.168.4.3  | 255.255.255.0    | 192.168.4.1          |                        |

На коммутаторах и роутере настроим:
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

### 2. Создадим сети VLAN и назначим их на порты коммутаторов:

Список VLAN и соответствие портов представлено в таблице:
| VLAN | Name       | Interface Assigned |
|------|------------|--------------------|
| 3    | Management | SW1: e0/0, e0/1    |
|      |            | SW2: e0/0          |
|      |            | SW1: e0/2          |
| 4    | Operations | SW2: e0/0, e0/1    |
| 8    | Native     | N/A                |

Конфигурацию портов покажем на SW2:
```
sh running-config interface et0/1
 !
 interface Ethernet0/1
 switchport access vlan 4
 switchport mode access
end
```

### 3. Настроим транк 802.1Q между коммутаторами: 

Пример конфигурации SW2:
```
sh running-config interface et0/0
!
switchport trunk encapsulation dot1q
 switchport trunk native vlan 8
 switchport mode trunk
 end
```
На SW1 встречный (et0/1) настроен аналогично.

### 4. Настроим маршрутизацию между VLAN на маршрутизаторе:

Конфигурация порта роутера R1 "смотрящего" (et0/0) на SW1:
```
interface Ethernet0/0
 no ip address
 no cdp enable
 no mop enabled
end
!
R1#sh running-config interface eth0/0.3
!
interface Ethernet0/0.3
 description MANAGEMENT
 encapsulation dot1Q 3
 ip address 192.168.3.1 255.255.255.0
 ipv6 address FE80::1 link-local
 ipv6 address FD00::1/64
 ipv6 enable
 no cdp enable
end
!
R1#sh running-config interface eth0/0.4
!
interface Ethernet0/0.4
 encapsulation dot1Q 4
 ip address 192.168.4.1 255.255.255.0
 no cdp enable
end
```
### 5. Проверим что маршрутизация между VLAN работает и задокументируем все изменеия:
Выполним следующие тесты на ПК-1. Все должно пройти успешно.
- Проверим связь с ПК-1 до шлюза по умолчанию;

```
VPCS> ping 192.168.3.1

192.168.3.1 icmp_seq=1 timeout
84 bytes from 192.168.3.1 icmp_seq=2 ttl=255 time=0.647 ms
84 bytes from 192.168.3.1 icmp_seq=3 ttl=255 time=0.547 ms
84 bytes from 192.168.3.1 icmp_seq=4 ttl=255 time=0.568 ms
84 bytes from 192.168.3.1 icmp_seq=5 ttl=255 time=0.586 ms
```
- Пинг с ПК-1 на ПК-2:

```
VPCS> ping 192.168.4.3

84 bytes from 192.168.4.3 icmp_seq=1 ttl=63 time=0.930 ms
84 bytes from 192.168.4.3 icmp_seq=2 ttl=63 time=0.904 ms
84 bytes from 192.168.4.3 icmp_seq=3 ttl=63 time=0.823 ms
84 bytes from 192.168.4.3 icmp_seq=4 ttl=63 time=1.045 ms
84 bytes from 192.168.4.3 icmp_seq=5 ttl=63 time=0.922 ms
```
- Пинг от ПК-1 к SW2:

```
VPCS> ping 192.168.3.12

84 bytes from 192.168.3.12 icmp_seq=1 ttl=255 time=0.376 ms
84 bytes from 192.168.3.12 icmp_seq=2 ttl=255 time=0.629 ms
84 bytes from 192.168.3.12 icmp_seq=3 ttl=255 time=0.669 ms
84 bytes from 192.168.3.12 icmp_seq=4 ttl=255 time=0.578 ms
84 bytes from 192.168.3.12 icmp_seq=5 ttl=255 time=0.581 ms
```

Все файлы изменений приведены [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_01/Config) 
![Итоговая схема:](https://github.com/Pekep97/Labs/blob/main/Lab_01/Lab_1.png)
