
### Шаг 1: Установка Suricata

1. **Обновите списки пакетов и установите Suricata:**
   ```bash
   sudo apt update
   sudo apt install suricata
   ```

2. **Проверьте статус Suricata после установки:**
   ```bash
   sudo systemctl status suricata
   ```

### Шаг 2: Добавление правила FIN/SYN сканирования

1. **Откройте файл правил Suricata:**
   ```bash
   sudo nano /etc/suricata/rules/local.rules
   ```

2. **Добавьте следующее правило для обнаружения FIN/SYN сканирования:**
   ```plaintext
   alert tcp any any -> any any (flags: F; msg: "FIN scan detected"; sid: 1000001; rev: 1;)
   alert tcp any any -> any any (flags: S; msg: "SYN scan detected"; sid: 1000002; rev: 1;)
   ```

3. **Сохраните изменения и закройте редактор (Ctrl + X, затем Y и Enter).**

### Шаг 3: Перезагрузка Suricata

1. **Перезагрузите службу Suricata, чтобы применить изменения:**
   ```bash
   sudo systemctl restart suricata
   ```

### Шаг 4: Запуск Kali Linux и сканирование виртуалки Suricata

1. **Запустите Kali Linux.**

2. **Проведите сканирование вашей виртуальной машины с помощью Nmap (например, для FIN и SYN сканирования):**
   ```bash
   nmap -sF [IP-адрес вашей виртуальной машины]
   nmap -sS [IP-адрес вашей виртуальной машины]
   ```


   ```
![image_2024-10-15_13-12-48](https://github.com/user-attachments/assets/ec22e9f1-f514-43db-a159-1b21a10b1fec)

