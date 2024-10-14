
### 1. Установка антивируса ClamAV с графической оболочкой и сканирование директории:

#### Установка ClamAV:

1. Обновите пакеты и установите ClamAV:
   ```bash
   sudo apt update
   sudo apt install clamav clamav-daemon
   ```

2. Обновите базы данных вирусных сигнатур:
   ```bash
   sudo freshclam
   ```

#### Установка графической оболочки для ClamAV:

Для ClamAV существует несколько графических интерфейсов, например *ClamTk*.

1. Установите ClamTk:
   ```bash
   sudo apt install clamtk
   ```

2. Запустите ClamTk из меню приложений или с помощью команды:
   ```bash
   clamtk
   ```

#### Сканирование любой директории:

1. Сканирование через командную строку:
   - Используйте команду `clamscan` для сканирования директории. Например, чтобы просканировать директорию `/home/user`:
     ```bash
     clamscan -r /home/user
     ```
   - Опция `-r` означает рекурсивное сканирование (включает все поддиректории).

2. Сканирование через ClamTk:
   - Откройте ClamTk, выберите опцию для сканирования и укажите директорию для проверки.

---

### 2. Установка YARA, вычисление хеша файла и создание правила:

#### Установка YARA:

1. Установите YARA:
   ```bash
   sudo apt update
   sudo apt install yara
   ```

#### Вычисление хеша для текстового файла:

1. Создайте текстовый файл:
   ```bash
   echo "This is a test file for YARA" > testfile.txt
   ```

2. Вычислите хеш файла, например с помощью команды `sha256sum`:
   ```bash
   sha256sum testfile.txt
   ```
   - Это выдаст хеш, который вам нужно использовать в правиле YARA.

#### Создание правила YARA:

1. Создайте файл `test_rule.yar` с содержимым:
   ```yara
   rule DetectTestFile {
       strings:
           $my_text = "This is a test file for YARA"
       condition:
           $my_text
   }
   ```

2. Запустите правило для сканирования директории с вашим файлом:
   ```bash
   yara test_rule.yar testfile.txt
   ```

   - Если правило найдено в файле, YARA покажет имя правила `DetectTestFile`.

---

### 3. Установка WAF (Nginx + ModSecurity):

#### Установка Nginx и ModSecurity:

1. Установите Nginx:
   ```bash
   sudo apt update
   sudo apt install nginx
   ```

2. Установите ModSecurity:
   ```bash
   sudo apt install libapache2-mod-security2
   ```

3. Настройте ModSecurity для использования с Nginx:
   - Установите необходимый модуль:
     ```bash
     sudo apt install libnginx-mod-security
     ```

4. Активируйте ModSecurity в конфигурации Nginx:
   - Откройте конфигурацию Nginx:
     ```bash
     sudo nano /etc/nginx/nginx.conf
     ```

   - Добавьте или раскомментируйте следующие строки в блоке `http`:
     ```nginx
     include /etc/nginx/modsecurity/modsecurity.conf;
     modsecurity on;
     modsecurity_rules_file /etc/nginx/modsecurity/custom_rules.conf;
     ```

   - Сохраните изменения и перезапустите Nginx:
     ```bash
     sudo systemctl restart nginx
     ```

#### Настройка правила для запрета тестового запроса:

1. Создайте файл правил `custom_rules.conf`:
   ```bash
   sudo nano /etc/nginx/modsecurity/custom_rules.conf
   ```

2. Добавьте правило для блокировки определенного запроса. Например, запрет на доступ к URL с определенным словом:
   ```modsecurity
   SecRule REQUEST_URI "@contains forbidden" "id:1001,phase:1,deny,status:403,msg:'Forbidden access detected'"
   ```

   - Это правило запрещает доступ ко всем URL, которые содержат слово "forbidden" и возвращает статус `403`.

3. Перезапустите Nginx, чтобы применить правило:
   ```bash
   sudo systemctl restart nginx
   ```

4. Тестирование правила:
   - Попробуйте обратиться к URL, содержащему "forbidden":
     ```bash
     curl http://your_server_ip/forbidden
     ```
   - Если правило работает, сервер вернет статус `403 Forbidden`.

---

Эти шаги помогут вам настроить и протестировать антивирус ClamAV, YARA и WAF на базе Nginx и ModSecurity. Если у вас возникнут дополнительные вопросы или проблемы, дайте знать!
