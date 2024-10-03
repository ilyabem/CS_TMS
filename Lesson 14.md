Создание скрипта для настройки `iptables` в формате `.sh` можно реализовать следующим образом:

### Шаги:
1. Очистка всех существующих правил `iptables`.
2. Добавление правил для разрешения соединений по портам 80 (HTTP) и 443 (HTTPS).
3. Ограничение доступа к порту 22 (SSH) только для внутренней сети.
4. Настройка NAT для всего исходящего трафика через интерфейс VM.
5. Установка UFW и повторение правил для iptables.

Ниже приведен пример скрипта `iptables_setup.sh`:

```bash
#!/bin/bash

# Очистка всех существующих правил
iptables -F
iptables -t nat -F
iptables -X

# Разрешить все соединения по 80 (HTTP) и 443 (HTTPS) портам
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Разрешить подключение к 22 порту только из внутренней сети (например, 192.168.1.0/24)
iptables -A INPUT -p tcp --dport 22 -s 192.168.1.0/24 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP

# Включить NAT для исходящего трафика через интерфейс eth0
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

# Установить UFW и активировать его
apt-get update && apt-get install ufw -y
ufw disable
ufw enable

# Настройка UFW для правил
ufw allow 80/tcp
ufw allow 443/tcp
ufw allow from 192.168.1.0/24 to any port 22

# Включение IP маскарадинга для NAT в UFW
echo "net/ipv4/ip_forward=1" >> /etc/ufw/sysctl.conf
ufw reload

# Показать итоговые правила iptables
iptables -L -v
iptables -t nat -L -v
```

### Описание шагов:
1. **Очистка правил**: Очищаются все текущие правила с помощью `iptables -F` и `iptables -X`.
2. **Правила для 80 и 443 портов**: Добавляются правила для разрешения входящих соединений на порты 80 и 443.
3. **SSH только для внутренней сети**: Разрешается подключение к порту 22 только для IP-адресов из диапазона 192.168.1.0/24. Все остальные запросы блокируются.
4. **NAT**: Включается NAT для всего исходящего трафика через интерфейс `eth0` с помощью `MASQUERADE`.
5. **UFW**: Устанавливается UFW (Uncomplicated Firewall), добавляются аналогичные правила для UFW, и активируется IP форвардинг для NAT.

Этот скрипт можно сохранить в файл `iptables_setup.sh` и выполнить с правами администратора (`sudo`):

```bash
sudo bash iptables_setup.sh
```

После выполнения скрипта, будут применены правила как для `iptables`, так и для `ufw`.
