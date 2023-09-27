# STP

### Задание:

1. Создание сети и настройка основных параметров устройства;
2. Выбор корневого моста;
3. Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов;
4. Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов;
5. Задокументировать все изменения.

### Решение:

1. [Создадим сеть и настроим основные параметры устройств;](https://github.com/Pekep97/Labs/tree/main/Lab_02#1-%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%B4%D0%B8%D0%BC-%D1%81%D0%B5%D1%82%D1%8C-%D0%B8-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B8%D0%BC-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-%D1%83%D1%81%D1%82%D1%80%D0%BE%D0%B9%D1%81%D1%82%D0%B2)
2. [Аргументируем выбор корневого моста;](https://github.com/Pekep97/Labs/tree/main/Lab_02#2-%D0%B0%D1%80%D0%B3%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%8B%D0%B1%D0%BE%D1%80-%D0%BA%D0%BE%D1%80%D0%BD%D0%B5%D0%B2%D0%BE%D0%B3%D0%BE-%D0%BC%D0%BE%D1%81%D1%82%D0%B0)
3. [Понаблюдаем за процессом выбора протоколом STP порта, исходя из стоимости портов;](https://github.com/Pekep97/Labs/tree/main/Lab_02#3-%D0%BF%D0%BE%D0%BD%D0%B0%D0%B1%D0%BB%D1%8E%D0%B4%D0%B0%D0%B5%D0%BC-%D0%B7%D0%B0-%D0%BF%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81%D0%BE%D0%BC-%D0%B2%D1%8B%D0%B1%D0%BE%D1%80%D0%B0-%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%D0%BE%D0%BC-stp-%D0%BF%D0%BE%D1%80%D1%82%D0%B0-%D0%B8%D1%81%D1%85%D0%BE%D0%B4%D1%8F-%D0%B8%D0%B7-%D1%81%D1%82%D0%BE%D0%B8%D0%BC%D0%BE%D1%81%D1%82%D0%B8-%D0%BF%D0%BE%D1%80%D1%82%D0%BE%D0%B2)
4. [Понаблюдаем за процессом выбора протоколом STP порта, исходя из приоритета портов и задокументируем все изменения.](https://github.com/Pekep97/Labs/tree/main/Lab_02#4-%D0%BF%D0%BE%D0%BD%D0%B0%D0%B1%D0%BB%D1%8E%D0%B4%D0%B0%D0%B5%D0%BC-%D0%B7%D0%B0-%D0%BF%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81%D0%BE%D0%BC-%D0%B2%D1%8B%D0%B1%D0%BE%D1%80%D0%B0-%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%D0%BE%D0%BC-stp-%D0%BF%D0%BE%D1%80%D1%82%D0%B0-%D0%B8%D1%81%D1%85%D0%BE%D0%B4%D1%8F-%D0%B8%D0%B7-%D0%BF%D1%80%D0%B8%D0%BE%D1%80%D0%B8%D1%82%D0%B5%D1%82%D0%B0-%D0%BF%D0%BE%D1%80%D1%82%D0%BE%D0%B2-%D0%B8-%D0%B7%D0%B0%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B5%D0%BC-%D0%B2%D1%81%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F)

### 1. Создадим сеть и настроим основные параметры устройств:

Исследуемая схема:

![Исследуемая схема:](https://github.com/Pekep97/Labs/blob/main/Lab_02/Lab3_STP.png)

Таблица адресации:

| Устройство | Интерфейс | IP-адрес    | Маска подсети |
|------------|-----------|-------------|---------------|
| SW1         | VLAN 1    | 192.168.1.1 | 255.255.255.0 |
| SW2         | VLAN 1    | 192.168.1.2 | 255.255.255.0 |
| SW3         | VLAN 1    | 192.168.1.3 | 255.255.255.0 |

На коммутаторах настроим:
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

### 2. Аргументируем выбор корневого моста:

В начале выполним следующие действия:
- отключим все порты на коммутаторах;
- настроим подключенные порты в качестве транковых;
- включим порты et0/1 и et0/3 на всех коммутаторах;
- отобразим данные протокола spanning-tree.

Данные протокола spanning-tree:

SW1:
```
SW1#sh spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.1000
             Cost        100
             Port        4 (Ethernet0/3)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.2000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/1               Desg FWD 100       128.2    Shr
Et0/3               Root FWD 100       128.4    Shr
```

SW2:
```
SW2#sh spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.1000
             Cost        100
             Port        4 (Ethernet0/3)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.4000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/1               Altn BLK 100       128.2    Shr
Et0/3               Root FWD 100       128.4    Shr
```

SW3:
```
SW3#sh spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.1000
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.1000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/1               Desg FWD 100       128.2    Shr
Et0/3               Desg FWD 100       128.4    Shr
```

По результатам видно:
- SW3 является корневым мостом (имеет наименьшее значение BID) и порты et0/1 и et0/3 являются корневыми портами;
- SW2 по результатам выборов имеет корневой порт et0/3, альтернативный порт et0/1;
- SW1 по результатам выборов имеет корневой порт et0/3, невыделенный порт et0/1.

### 3. Понаблюдаем за процессом выбора протоколом STP порта, исходя из стоимости портов:

При текущей конфигурации только один коммутатор может содержать заблокированный протоколом STP порт с самым высоким идентификатором BID (SW2:et0/1).
- Изменим стоимость корневого порта (SW2:et0/3) на равную 5 командой 
```
SW2(config)#interface ethernet 0/3
SW2(config-if)#shut
SW2(config-if)#spanning-tree cost 5
SW2(config-if)#no shut
```

- Покажем значения spanning tree на некорневых коммутаторах:

SW1:
```
SW1#sh span

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.1000
             Cost        100
             Port        4 (Ethernet0/3)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.2000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/1               Altn BLK 100       128.2    Shr
Et0/3               Root FWD 100       128.4    Shr
```

SW2:
```
SW2#sh spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.1000
             Cost        5
             Port        4 (Ethernet0/3)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.4000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/1               Desg FWD 100       128.2    Shr
Et0/3               Root FWD 5         128.4    Shr
```

- Удалим изменения стоимости порта и покажем что протокол STP сбросил порт на коммутаторе некорневого моста, вернув исходные настройки порта:
```
SW2(config)#interface ethernet 0/3
SW2(config-if)#shut
SW2(config-if)#no spanning-tree cost
SW2(config-if)#no shut
```

SW2
```
SW2#sh spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.1000
             Cost        100
             Port        4 (Ethernet0/3)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.4000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/1               Altn BLK 100       128.2    Shr
Et0/3               Root FWD 100       128.4    Shr
```

### 4. Понаблюдаем за процессом выбора протоколом STP порта, исходя из приоритета портов и задокументируем все изменения:

- Активируем избыточные порты (et0/0 и et0/2) на коммутаторах и покажем результат работы STP:

SW1
```
SW1#sh spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.1000
             Cost        100
             Port        3 (Ethernet0/2)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.2000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Desg FWD 100       128.1    Shr
Et0/1               Desg FWD 100       128.2    Shr
Et0/2               Root FWD 100       128.3    Shr
Et0/3               Altn BLK 100       128.4    Shr
```

SW2
```
SW2#sh spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.1000
             Cost        100
             Port        3 (Ethernet0/2)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.4000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Altn BLK 100       128.1    Shr
Et0/1               Altn BLK 100       128.2    Shr
Et0/2               Root FWD 100       128.3    Shr
Et0/3               Altn BLK 100       128.4    Shr
```

SW3
```
SW3#sh spanning-tree

VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     aabb.cc00.1000
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.1000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Desg FWD 100       128.1    Shr
Et0/1               Desg FWD 100       128.2    Shr
Et0/2               Desg FWD 100       128.3    Shr
Et0/3               Desg FWD 100       128.4    Shr
```

- Покажем связность сети утилитой ping на SW1:
```
SW1#ping 192.168.1.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.2, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 1/1/1 ms
SW1#ping 192.168.1.3
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.3, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 1/1/1 ms
```

Вопросы для повторения:

1. Какое значение протокол STP использует первым после выбора корневого моста, чтобы определить выбор порта?
Ответ: суммарный RPC.

3. Если первое значение на двух портах одинаково, какое следующее значение будет использовать протокол STP при выборе порта?
Ответ: Bridge ID.

4. Если оба значения на двух портах равны, каким будет следующее значение, которое использует протокол STP при выборе порта?
Ответ: Port ID.

Все файлы изменений приведены [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_02/Configs)
