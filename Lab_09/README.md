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

|          |            |               | Москва       |                       |         |                    |             |                |
|----------|------------|---------------|--------------|-----------------------|---------|--------------------|-------------|----------------|
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R14      | e0/2       | l3:to-AS-101  | 85.10.22.2   | 255.255.255.252 (/30) | -       | 2000:0:1001:101::2 | /112        | fe80::2        |
| R15      | e0/2       | l3:to-AS-301  | 132.50.21.2  | 255.255.255.252 (/30) | -       | 2000:0:1001:301::2 | /112        | fe80::2        |
|          |            |               | Киторн       |                       |         |                    |             |                |
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R22      | e0/0       | l3:to-AS-1001 | 85.10.22.1   | 255.255.255.252 (/30) | -       | 2000:0:1001:101::1 | /112        | fe80::1        |
|          | e0/1       | l3:to-AS-301  | 21.22.100.1  | 255.255.255.252 (/30) | -       | 2000:0:301:101::1  | /112        | fe80::2        |
|          |            |               | Ламас        |                       |         |                    |             |                |
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R21      | e0/0       | l3:to-AS-1001 | 132.50.21.1  | 255.255.255.252 (/30) | -       | 2000:0:1001:301::1 | /112        | fe80::1        |
|          | e0/1       | l3:to-AS-101  | 21.22.100.2  | 255.255.255.252 (/30) | -       | 2000:0:301:101::2  | /112        | fe80::1        |
|          | e0/2       | l3:to-AS-520  | 24.100.40.2  | 255.255.255.252 (/30) | -       | 2000:0:520:301::2  | /112        | fe80::1        |
|          |            |               | Триада       |                       |         |                    |             |                |
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R24      | e0/0       | l3:to-AS-301  | 24.100.40.1  | 255.255.255.252 (/30) | -       | 2000:0:520:301::1  | /112        | fe80::2        |
|          | e0/3       | l3:to-AS-2042 | 24.100.40.5  | 255.255.255.252 (/30) | -       | 2000:0:520:2042::1 | /112        | fe80::2        |
|          |            |               | С.-Петербург |                       |         |                    |             |                |
| Hostname | Interfaces | Description   | IPv4-address | Mask                  | Gateway | IPv6-address       | IPv6-prefix | LLIPv6-address |
| R18      | e0/2       | l3:to-AS-520  | 24.100.40.6  | 255.255.255.252 (/30) | -       | 2000:0:520:2042::2 | /112        | fe80::1        |
|          | e0/3       | l3:to-AS-520  | 26.100.40.2  | 255.255.255.252 (/30) | -       | 2000:0:2042:520::2 | /112        | fe80::2        |

- Покажем настройки eBGP между офисом Москва и двумя провайдерами - Киторн и Ламас на маршрутизаторе в офисе Москва R14:

*IPv4*
```

```