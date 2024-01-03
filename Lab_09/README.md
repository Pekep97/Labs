# eBGP

### Задание:

1. Настройте eBGP между офисом Москва и двумя провайдерами - Киторн и Ламас;
2. Настройте eBGP между провайдерами Киторн и Ламас;
3. Настройте eBGP между Ламас и Триада;
4. Настройте eBGP между офисом С.-Петербург и провайдером Триада;
5. Организуйте IP доступность между пограничным роутерами офисами Москва и С.-Петербург.

### Решение: 

1. Настроим eBGP между офисом Москва и двумя провайдерами - Киторн и Ламас;
2. Настроим eBGP между провайдерами Киторн и Ламас;
3. Настроим eBGP между Ламас и Триада;
4. Настроим eBGP между офисом С.-Петербург и провайдером Триада;
5. Организуем IP доступность между пограничным роутерами офисами Москва и С.-Петербург и задокументируем все изменения.

1. Настроим eBGP между офисом Москва и двумя провайдерами - Киторн и Ламас;

- Исследуемая схема описана [тут.](https://github.com/Pekep97/Labs/tree/main/Lab_04) Для упрощения понимания задублируем в этой работе только нужное:

### Исследуемая схема:

![Исследуемая схема](https://github.com/Pekep97/Labs/blob/main/Lab_04/Lab_04.png)

### Таблица адресного пространства:

|          |            |               | ***Москва***       |                       |         |                    |             |                |
|----------|------------|---------------|--------------|-----------------------|---------|--------------------|-------------|----------------|
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R14      | e0/2       | l3:to-AS-101  | 85.10.22.2   | 255.255.255.252 (/30) | -       | 2000:0:1001:101::2 | /112        | fe80::2        |
| R15      | e0/2       | l3:to-AS-301  | 132.50.21.2  | 255.255.255.252 (/30) | -       | 2000:0:1001:301::2 | /112        | fe80::2        |
|          |            |               | Киторн       |                       |         |                    |             |                |
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R22      | e0/0       | l3:to-AS-1001 | 85.10.22.1   | 255.255.255.252 (/30) | -       | 2000:0:1001:101::1 | /112        | fe80::1        |
|          | e0/1       | l3:to-AS-301  | 21.22.100.1  | 255.255.255.252 (/30) | -       | 2000:0:301:101::1  | /112        | fe80::2        |
|          |            |               | ***Ламас***        |                       |         |                    |             |                |
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R21      | e0/0       | l3:to-AS-1001 | 132.50.21.1  | 255.255.255.252 (/30) | -       | 2000:0:1001:301::1 | /112        | fe80::1        |
|          | e0/1       | l3:to-AS-101  | 21.22.100.2  | 255.255.255.252 (/30) | -       | 2000:0:301:101::2  | /112        | fe80::1        |
|          | e0/2       | l3:to-AS-520  | 24.100.40.2  | 255.255.255.252 (/30) | -       | 2000:0:520:301::2  | /112        | fe80::1        |
|          |            |               | ***Триада***       |                       |         |                    |             |                |
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R24      | e0/0       | l3:to-AS-301  | 24.100.40.1  | 255.255.255.252 (/30) | -       | 2000:0:520:301::1  | /112        | fe80::2        |
|          | e0/3       | l3:to-AS-2042 | 24.100.40.5  | 255.255.255.252 (/30) | -       | 2000:0:520:2042::1 | /112        | fe80::2        |
|          |            |               | ***С.-Петербург*** |                       |         |                    |             |                |
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R18      | e0/2       | l3:to-AS-520  | 24.100.40.6  | 255.255.255.252 (/30) | -       | 2000:0:520:2042::2 | /112        | fe80::1        |
|          | e0/3       | l3:to-AS-520  | 26.100.40.2  | 255.255.255.252 (/30) | -       | 2000:0:2042:520::2 | /112        | fe80::2        |

- Покажем настройки eBGP между офисом Москва и провайдером Киторн на маршрутизаторе офиса Москва R14 и на маршрутизаторе офиса Киторн R22:

*R14*
```
R14#sh run | sec bgp
router bgp 1001
 bgp router-id 14.14.14.14
 bgp log-neighbor-changes
 neighbor 2000:0:1001:101::1 remote-as 101
 neighbor 85.10.22.1 remote-as 101
 !
 address-family ipv4
  no neighbor 2000:0:1001:101::1 activate
  neighbor 85.10.22.1 activate
  neighbor 85.10.22.1 next-hop-self
 exit-address-family
 !
 address-family ipv6
  neighbor 2000:0:1001:101::1 activate
  neighbor 2000:0:1001:101::1 next-hop-self
 exit-address-family
```

*R22*
```
R22#sh run | sec bgp
router bgp 101
 bgp router-id 22.22.22.22
 bgp log-neighbor-changes
 neighbor 21.22.100.2 remote-as 301
 neighbor 2000:0:301:101::2 remote-as 301
 neighbor 2000:0:1001:101::2 remote-as 1001
 neighbor 85.10.22.2 remote-as 1001
 !
 address-family ipv4
  network 85.10.22.0 mask 255.255.255.252
  neighbor 21.22.100.2 activate
  no neighbor 2000:0:301:101::2 activate
  no neighbor 2000:0:1001:101::2 activate
  neighbor 85.10.22.2 activate
 exit-address-family
 !
 address-family ipv6
  network 2000:0:1001:101::/112
  neighbor 2000:0:301:101::2 activate
  neighbor 2000:0:1001:101::2 activate
 exit-address-family
```

- Покажем вывод команды *sh ip bgp* на маршрутизаторе R14:

```
R14#sh ip bgp
BGP table version is 19, local router ID is 14.14.14.14
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 r>  85.10.22.0/30    85.10.22.1               0             0 101 i
 *>  132.50.21.0/30   85.10.22.1                             0 101 301 i
```

### 2. Настроим eBGP между провайдерами Киторн и Ламас:

- Покажем конфигурацию маршрутизатора офиса Ламас R21:

*R21*
```
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
  network 132.50.21.0 mask 255.255.255.252
  neighbor 21.22.100.1 activate
  neighbor 24.100.40.1 activate
  no neighbor 2000:0:301:101::1 activate
  no neighbor 2000:0:520:301::1 activate
  no neighbor 2000:0:1001:301::2 activate
  neighbor 132.50.21.2 activate
 exit-address-family
 !
 address-family ipv6
  network 2000:0:1001:301::/112
  neighbor 2000:0:301:101::1 activate
  neighbor 2000:0:520:301::1 activate
  neighbor 2000:0:1001:301::2 activate
 exit-address-family
```

- Покажем вывод команды *sh ip bgp* на маршрутизаторе R21:

```
R21#sh ip bgp
BGP table version is 20, local router ID is 21.21.21.21
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *>  85.10.22.0/30    21.22.100.1              0             0 101 i
 *>  132.50.21.0/30   0.0.0.0                  0         32768 i
```

### 3. Настроим eBGP между Ламас и Триада:

- Покажем конфигурацию маршрутизатора офиса Триада R24

*R24*
```
R24#sh run | sec bgp
router bgp 520
 bgp router-id 24.24.24.24
 bgp log-neighbor-changes
 neighbor 24.100.40.2 remote-as 301
 neighbor 24.100.40.6 remote-as 2042
 neighbor 2000:0:520:301::2 remote-as 301
 neighbor 2000:0:520:2042::2 remote-as 2042
 !
 address-family ipv4
  network 24.100.40.4 mask 255.255.255.252
  neighbor 24.100.40.2 activate
  neighbor 24.100.40.6 activate
  no neighbor 2000:0:520:301::2 activate
  no neighbor 2000:0:520:2042::2 activate
 exit-address-family
 !
 address-family ipv6
  network 2000:0:520:2042::/112
  neighbor 2000:0:520:301::2 activate
  neighbor 2000:0:520:2042::2 activate
 exit-address-family
```

- Покажем вывод команды *sh ip bgp* на маршрутизаторе R24:
```
R24#sh ip bgp
BGP table version is 4, local router ID is 24.24.24.24
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 *>  24.100.40.4/30   0.0.0.0                  0         32768 i
 *>  85.10.22.0/30    24.100.40.2                            0 301 101 i
 *>  132.50.21.0/30   24.100.40.2              0             0 301 i
```

### 4. Настроим eBGP между офисом С.-Петербург и провайдером Триада:

- Покажем конфигурацию маршрутизатора офиса С.-Петербург R18:

*R18*
```
R18#sh run | sec bgp
router bgp 2042
 bgp router-id 18.18.18.18
 bgp log-neighbor-changes
 neighbor 24.100.40.5 remote-as 520
 neighbor 2000:0:520:2042::1 remote-as 520
 !
 address-family ipv4
  neighbor 24.100.40.5 activate
  neighbor 24.100.40.5 next-hop-self
  no neighbor 2000:0:520:2042::1 activate
 exit-address-family
 !
 address-family ipv6
  neighbor 2000:0:520:2042::1 activate
  neighbor 2000:0:520:2042::1 next-hop-self
 exit-address-family
```

- Покажем вывод команды *sh ip bgp* на маршрутизаторе R18:
```
R18#sh ip bgp
BGP table version is 4, local router ID is 18.18.18.18
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
              x best-external, a additional-path, c RIB-compressed,
Origin codes: i - IGP, e - EGP, ? - incomplete
RPKI validation codes: V valid, I invalid, N Not found

     Network          Next Hop            Metric LocPrf Weight Path
 r>  24.100.40.4/30   24.100.40.5              0             0 520 i
 *>  85.10.22.0/30    24.100.40.5                            0 520 301 101 i
 *>  132.50.21.0/30   24.100.40.5                            0 520 301 i
```

### 5. Организуем IP доступность между пограничными роутерами офисами Москва и С.-Петербург и задокументируем все изменения:

- Для организации IP доступности между пограничными роутерами офисами Москва и С.-Петербург необходимо:

  * на маршрутизаторах офисов Киторн (R22), Ламас (R21) и Триада (R24) анонсировать стыковочные сети в протокол BGP командой *network*

- Покажем результат выполнения утилиты *ping* на маршрутизаторы офиса Москва (R14, R15) с маршрутизатора офиса С.-Петербург (R18):

*IPv4*
```
R18#ping 85.10.22.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 85.10.22.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
--------------------
R18#ping 132.50.21.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 132.50.21.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
```

*IPv6*
```
R18#ping 2000:0:1001:301::2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2000:0:1001:301::2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
--------------------
R18#ping 2000:0:1001:101::2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2000:0:1001:101::2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/1/1 ms
```

Все изменения задокументированы здесь.
