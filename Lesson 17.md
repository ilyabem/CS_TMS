

### 1. Скачать образ Ubuntu 18.04 с Docker Hub и проверить его целостность:

- Скачайте образ с Docker Hub с помощью команды:

```bash
docker pull ubuntu:18.04
```

- После загрузки получите контрольную сумму SHA256 для образа:

```bash
docker image inspect ubuntu:18.04 --format='{{.ID}}'
```
![image](https://github.com/user-attachments/assets/bd5c2923-9522-4a07-8032-4a9eddf1bfdf)
- Сравните полученную контрольную сумму с опубликованной на Docker Hub на странице образа. Если контрольные суммы совпадают, это подтверждает целостность образа.

### 2. Отобразить все Docker-образы на системе:

- Для отображения всех Docker-образов используйте:

```bash
docker image ls
```
![docker image ls](https://github.com/user-attachments/assets/5b6cde27-8df2-4fc1-978c-6f3ad6cb74cc)

### 3. Добавить пользователя в группу `docker` для запуска команд без `sudo`:

- Добавьте вашего пользователя в группу `docker`:

```bash
sudo usermod -aG docker $USER
```

- Затем примените изменения:

```bash
newgrp docker
```

Или перезагрузите систему, чтобы изменения вступили в силу.

### 4. Запустить образ в интерактивном режиме:

- Запустите контейнер с образом Ubuntu 18.04 в интерактивном режиме с оболочкой `sh`:

```bash
docker run -it ubuntu:18.04 sh
```

### 5. Определить пользователя внутри контейнера:

- Выполните команду `whoami` внутри контейнера, чтобы увидеть, от имени какого пользователя работает контейнер:

```bash
whoami
```
![photo_2024-10-14_14-39-43](https://github.com/user-attachments/assets/cc35d8dd-aaf1-4355-8b6d-211fd558bda9)

Ожидаемый результат: `root` (так как контейнеры Docker по умолчанию запускаются с правами суперпользователя).

### 6. Запустить контейнер под пользователем `tms`:

- Создайте пользователя `tms` внутри контейнера и запустите оболочку под этим пользователем:

```bash
docker run -it ubuntu:18.04 /bin/bash
```

Затем внутри контейнера выполните следующие команды:

```bash
apt update && apt install -y sudo
useradd -m tms
passwd tms
usermod -aG sudo tms
su - tms
```
![црщфьш](https://github.com/user-attachments/assets/5dda502d-abf4-4c19-8039-a0cf345577a6)

Теперь вы вошли под пользователем `tms`.

### 7. Прогонка образа через один из сканеров безопасности:

Для этого можно использовать один из следующих инструментов:

- **Trivy**:
  
  1. Установите Trivy:

     ```bash
     curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sudo sh -s -- -b /usr/local/bin
     ```

  2. Запустите сканирование образа:

     ```bash
     trivy image ubuntu:18.04
     ```
![image](https://github.com/user-attachments/assets/24915f98-2e14-4985-a9ce-34f5cc61ea88)
