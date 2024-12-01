1 Написать красочный интерактивный python-script для
автоматизации ваших часто повторяемых действий, либо
парсинга сайта для получения нужной информации
### Этот Python-скрипт автоматизирует задачи, связанные с запуском приложений, взаимодействием с Telegram-ботом , для ежедневного входа и чекина и использования билетов blum 

```python
import pyautogui
import time
import os
import subprocess
import keyboard  # Для отслеживания нажатия пробела

# Открываем Проводник
def open_explorer_and_run():
    subprocess.Popen('explorer')  # Это откроет Проводник Windows
    time.sleep(5)  # Ждем 5 секунд, пока откроется Проводник

    # Переходим к нужной директории
    path_to_file = r'C:\Users\User\Downloads\Telegram Desktop\blum v2.exe'  # Укажите путь к blum.exe
    os.startfile(path_to_file)  # Открываем файл
    time.sleep(5)  # Ждем 5 секунд, пока файл откроется

    # Сворачиваем Проводник
    pyautogui.hotkey('win', 'd')  # Это нажимает Win + D для сворачивания всех окон (включая Проводник)
    time.sleep(2)  # Ждем 2 секунды, чтобы Проводник свернулся

def open_telegram():
    # Открываем Telegram
    subprocess.Popen(r"D:\Telegram Desktop\Telegram.exe")  # Укажите путь к Telegram.exe
    time.sleep(5)  # Ждем 5 секунд, пока откроется приложение

def open_chat_and_start():
    # Открываем чат через горячие клавиши
    pyautogui.hotkey('ctrl', 'f')  # Нажимаем Ctrl + F для поиска чата
    time.sleep(1)

    # Печатаем название чата "Blum"
    pyautogui.write("Blum")
    time.sleep(2)  # Ждем 2 секунды для того, чтобы чат отобразился

    # Нажимаем на чат
    pyautogui.press('enter')  # Открываем чат
    time.sleep(2)  # Ждем 2 секунды, пока чат откроется

    # Вводим команду /start
    pyautogui.write("/start")
    pyautogui.press('enter')
    time.sleep(5)  # Ждем 5 секунд для выполнения команды

def click_coordinates():
    # Выполняем клик по координатам (931, 923)
    pyautogui.click(931, 923)  # Клик по указанным координатам
    time.sleep(2)  # Пауза, чтобы клик успел сработать

    # Ждем 5 секунд после клика
    time.sleep(5)

    # Кликаем по координатам (938, 781)
    pyautogui.click(930, 716)
    time.sleep(2)  # Ждем 2 секунды

    # Второй клик по тем же координатам (938, 781)
    pyautogui.click(930, 716)
    time.sleep(2)  # Ждем 2 секунды

    # Поднимаемся до координат (925, 622)
    pyautogui.moveTo(925, 622)  # Поднимаем курсор
    time.sleep(1)  # Ждем 1 секунду

    # Скроллим вниз
    pyautogui.scroll(-200)  # Скроллим вниз (можно настроить значение прокрутки)
    time.sleep(1)  # Ждем 1 секунду

    # Кликаем по координатам (1050, 623)
    pyautogui.click(1050, 623)
    time.sleep(2)  # Ждем 2 секунды

    # Нажимаем клавишу 1
    pyautogui.press('1')
    time.sleep(2)  # Ждем 2 секунды

    # Ждем 35 секунд
    time.sleep(35)

    # Кликаем по координатам (985, 780)
    pyautogui.click(985, 780)
    time.sleep(2)  # Ждем 2 секунды

def click_forever():
    while True:
        if keyboard.is_pressed('space'):  # Проверяем, была ли нажата клавиша пробела
            print("Цикл завершен!")
            break  # Если пробел, выходим из цикла
        pyautogui.click(985, 780)  # Клик по координатам
        time.sleep(35)  # Пауза 35 секунд

def main():
    open_explorer_and_run()  # Открыть Проводник и запустить blum v2.exe
    open_telegram()  # Открыть Telegram
    open_chat_and_start()  # Открыть чат с ботом Blum и ввести команду /start
    click_coordinates()  # Выполнить все клики по экранам
    click_forever()  # Начать зацикленное нажатие с возможностью прерывания пробелом

if __name__ == "__main__":
    main()
```

---

### Инструкция по установке и запуску

#### 1. Установите Python
   - Скачайте Python с [официального сайта](https://www.python.org/).
   - При установке выберите "Add Python to PATH".

#### 2. Установите зависимости
   - В командной строке выполните:
     ```bash
     pip install pyautogui keyboard
     ```

#### 3. Настройте пути
   - Измените пути к `Telegram.exe` и `blum v2.exe` в коде.

#### 4. Запустите скрипт
   - Сохраните код в файл `main.py`.
   - В командной строке выполните:
     ```bash
     python main.py
     ```

#### 5. Конвертация в `.exe` (опционально)
   - Установите `pyinstaller`:
     ```bash
     pip install pyinstaller
     ```
   - Сконвертируйте в `.exe`:
     ```bash
     pyinstaller --onefile main.py
     ```
   - Запустите `.exe` файл из папки `dist`.
