Давайте разберем по пунктам:

### 1. Установка двухфакторной аутентификации (2FA) на Linux с использованием Google Authenticator

Для установки Google Authenticator на Linux и настройки двухфакторной аутентификации (2FA), выполните следующие шаги:

#### Шаги для настройки Google Authenticator:

1. Установите пакет `libpam-google-authenticator`:

   ```bash
   sudo apt update
   sudo apt install libpam-google-authenticator
   ```

2. Настройте Google Authenticator:

   Выполните команду:

   ```bash
   google-authenticator
   ```

   В процессе настройки вам будут предложены различные параметры:
   - Создание секретного ключа.
   - Генерация QR-кода, который нужно будет отсканировать с помощью приложения Google Authenticator на смартфоне.
   - Ответы на вопросы о конфигурации (рекомендуется использовать стандартные настройки).

3. Настройка PAM для включения двухфакторной аутентификации:

   Откройте файл `/etc/pam.d/sshd`:

   ```bash
   sudo nano /etc/pam.d/sshd
   ```

   Добавьте в начало файла:

   ```
   auth required pam_google_authenticator.so
   ```

4. Разрешите двухфакторную аутентификацию в настройках SSH:

   Откройте файл `/etc/ssh/sshd_config`:

   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

   Найдите строку и измените на `yes`:

   ```
   ChallengeResponseAuthentication yes
   ```

   Затем перезапустите SSH:

   ```bash
   sudo systemctl restart sshd
   ```

5. Теперь, при подключении по SSH, система будет запрашивать код двухфакторной аутентификации из приложения Google Authenticator.

   
![verif](https://github.com/user-attachments/assets/0b49dff6-e26c-4d8f-a340-de1b23eb542b)
![open](https://github.com/user-attachments/assets/9fb862e2-471a-473b-9cf1-22a225c5fd4c)

