### Скрипт: `install_menu.sh`

Этот скрипт написан на Bash для автоматизации часто повторяемых задач на системе Ubuntu. Он предоставляет удобное интерактивное меню для выполнения следующих действий:

- Проверка и устранение блокировки apt.
- Обновление системы (`apt update` и `apt upgrade`).
- Установка популярных утилит: `wget`, `curl`, `docker`, `docker-compose`.

### Назначение
Скрипт упрощает управление системой Ubuntu, экономит время на выполнение рутинных задач и снижает вероятность ошибок ручного ввода.

---

### Код скрипта

```bash
#!/bin/bash

# Скрипт автоматизации установки и обновления ПО для Ubuntu

# Проверка и устранение блокировки apt
check_apt_lock() {
    if sudo lsof /var/lib/dpkg/lock-frontend >/dev/null 2>&1; then
        echo "Блокировка apt обнаружена."
        LOCK_PID=$(sudo lsof -t /var/lib/dpkg/lock-frontend)
        LOCK_CMD=$(ps -p $LOCK_PID -o comm=)
        echo "Процесс $LOCK_CMD (PID: $LOCK_PID) удерживает блокировку."
        echo -n "Хотите завершить процесс? (y/n): "
        read -r choice
        if [[ $choice == "y" ]]; then
            sudo kill "$LOCK_PID"
            echo "Процесс завершен. Блокировка снята."
        else
            echo "Ожидание завершения процесса..."
            while sudo lsof /var/lib/dpkg/lock-frontend >/dev/null 2>&1; do
                sleep 5
            done
            echo "Блокировка снята."
        fi
    fi
}

# Обновление системы
update_system() {
    echo "Обновление системы..."
    sudo apt update && sudo apt upgrade -y
    echo "Система обновлена."
}

# Установка пакета с проверкой
install_package() {
    PACKAGE=$1
    if dpkg -l | grep -q "^ii  $PACKAGE "; then
        echo "Утилита $PACKAGE уже установлена."
    else
        echo "Устанавливаю $PACKAGE..."
        sudo apt install -y "$PACKAGE"
        echo "Утилита $PACKAGE успешно установлена."
    fi
}

# Главное меню
while true; do
    echo "======================================="
    echo "          Меню установки утилит"
    echo "======================================="
    echo "1) Обновить систему"
    echo "2) Установить wget"
    echo "3) Установить curl"
    echo "4) Установить Docker"
    echo "5) Установить Docker Compose"
    echo "6) Выход"
    echo -n "Выберите действие (1-6): "
    read -r choice

    case $choice in
        1)
            check_apt_lock
            update_system
            ;;
        2)
            check_apt_lock
            install_package wget
            ;;
        3)
            check_apt_lock
            install_package curl
            ;;
        4)
            check_apt_lock
            install_package docker.io
            ;;
        5)
            check_apt_lock
            install_package docker-compose
            ;;
        6)
            echo "Выход из программы."
            break
            ;;
        *)
            echo "Неверный выбор. Попробуйте снова."
            ;;
    esac
    echo
done
```

---

### Инструкция по использованию

2. **Сделайте его исполняемым:**
   ```bash
   chmod +x install_menu.sh
   ```

3. **Запустите скрипт:**
   ```bash
   ./install_menu.sh
   ```

---

### Описание работы

1. **Проверка блокировки apt:**
   Если процесс блокирует `apt`, скрипт предлагает завершить этот процесс или подождать, пока блокировка исчезнет.

2. **Обновление системы:**
   Выполняются команды `sudo apt update` и `sudo apt upgrade -y` для обновления всех установленных пакетов.

3. **Установка утилит:**
   Для каждой утилиты (например, `wget`, `curl`) проверяется, установлена ли она. Если нет, скрипт автоматически её устанавливает.

4. **Интерактивное меню:**
   Пользователь выбирает действия через удобное текстовое меню.
![1](https://github.com/user-attachments/assets/ecd11726-ed6b-4f70-bd8a-47dce7b4e47a)


   
### Скрипт: `SystemUtilityMenu`

Данный PowerShell-скрипт предоставляет интерактивное меню для установки программ через пакетный менеджер Chocolatey и отображения системной информации. Скрипт состоит из двух функций и главного меню:

1. **Install-Program**: Устанавливает указанные программы через Chocolatey. Проверяет, установлена ли программа, и, если нет, производит её установку.
2. **Show-SystemInfo**: Выводит информацию о системе, включая название процессора, объем оперативной памяти и свободное место на дисках.
3. **Главное меню**: Позволяет пользователю выбрать действие (установить программу или вывести системную информацию).

### Функции скрипта
- **Установка программ**: Позволяет установить Google Chrome или Visual Studio Code.
- **Информация о системе**: Отображает данные о процессоре, памяти и свободном месте.
- **Интерактивность**: Пользователь может легко выбирать действия через меню.

### Как использовать
1. Убедитесь, что Chocolatey установлен.
2. Скопируйте скрипт в `.ps1` файл (например, `SystemUtilityMenu.ps1`).
3. Запустите PowerShell от имени администратора.
4. Выполните скрипт с помощью команды:  
   ```powershell
   ./SystemUtilityMenu.ps1
   ```

### Код 

```powershell
# Функция установки программы через Chocolatey
function Install-Program {
    param(
        [string]$ProgramName
    )
    if (choco list --localonly | Select-String -Pattern $ProgramName) {
        Write-Host "$ProgramName уже установлен."
    } else {
        Write-Host "Устанавливаем $ProgramName..."
        choco install $ProgramName -y
        Write-Host "$ProgramName успешно установлен."
    }
}

# Функция вывода системной информации
function Show-SystemInfo {
    Write-Host "=== Информация о системе ==="
    Write-Host "Процессор: $(Get-CimInstance Win32_Processor | Select-Object -ExpandProperty Name)"
    Write-Host "Оперативная память: $(Get-CimInstance Win32_PhysicalMemory | Measure-Object Capacity -Sum | ForEach-Object {($_.Sum / 1GB) -as [int]}) GB"
    Write-Host "Свободное место на дисках:"
    Get-PSDrive -PSProvider FileSystem | ForEach-Object {
        Write-Host "$($_.Name): $([math]::round($_.Free / 1GB, 2)) GB свободно из $([math]::round($_.Used / 1GB + $_.Free / 1GB, 2)) GB"
    }
}

# Главное меню
while ($true) {
    Write-Host "=== Меню управления ==="
    Write-Host "1) Установить Google Chrome"
    Write-Host "2) Установить Visual Studio Code"
    Write-Host "3) Показать системную информацию"
    Write-Host "4) Выйти"
    $choice = Read-Host "Выберите действие (1-4)"

    switch ($choice) {
        1 { Install-Program "googlechrome" }
        2 { Install-Program "vscode" }
        3 { Show-SystemInfo }
        4 { Write-Host "Выход из программы."; break }
        default { Write-Host "Неверный выбор. Попробуйте снова." }
    }
    Write-Host ""
}
```
![2](https://github.com/user-attachments/assets/1f3ad305-e725-4d6d-8f03-0915d97e8c0f)

