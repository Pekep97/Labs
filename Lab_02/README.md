# STP

### Задание:

1. Создание сети и настройка основных параметров устройства;
2. Выбор корневого моста;
3. Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов;
4. Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов;
5. Задокументировать все изменения.

### Решение:

1. Создадим сеть и настроим основные параметры устройств;
2. Аргументируем выбор корневого моста;
3. Понаблюдаем за процессом выбора протоколом STP порта, исходя из стоимости портов;
4. Понаблюдаем за процессом выбора протоколом STP порта, исходя из приоритета портов и задокументируем все изменения.

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
- Изменим стоимость корневого порта (SW2:et0/3) на равную 200000000 командой 
```
SW2(config)#interface ethernet 0/3
SW2(config-if)#shut
SW2(config-if)#spanning-tree cost 200000000
SW2(config-if)#no shut
```

- Покажем значения spanning tree на некорневых коммутаторах:

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
             Cost        200
             Port        2 (Ethernet0/1)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     aabb.cc00.4000
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/1               Root FWD 100       128.2    Shr
Et0/3               Altn BLK 200000000 128.4    Shr
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

Активируем избыточные порты (et0/0 и et0/2) на коммутаторах и покажем результат работы STP:

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

Все файлы изменений приведены [здесь.](https://github.com/Pekep97/Labs/tree/main/Lab_01/Config)
