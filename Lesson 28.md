Установить SSDEEP на Linux

●Создать файл test.txt, добавить в него произвольный код

●Скопировать test.txt в файл bamboo.exe, добавить 1 символ в конец
файла bamboo.exe: echo “1” >> bamboo.exe

●Вычислить hash test.txt, hash до и после изменения bamboo.exe

●C помощью SSDEEP сравнить два файла
![photo_2024-12-01_13-21-38](https://github.com/user-attachments/assets/3a39d6b6-125a-4729-b213-161541ae50e5)
#### 1. **Установка SSDEEP на Linux**  

1. Убедитесь, что ваша система поддерживает установку `ssdeep`. Введите команду:  
   ```bash
   sudo apt update
   sudo apt install ssdeep
   ```

2. Проверьте установку:  
   ```bash
   ssdeep -h
   ```

---

#### 3. **Создание и работа с файлами**

##### Создание `test.txt`:
```bash
echo "This is a test file" > test.txt
```

##### Копирование файла и внесение изменений:
```bash
cp test.txt bamboo.exe
echo "1" >> bamboo.exe
```

---

#### 4. **Вычисление хэшей**  

##### Хэширование `test.txt`:
```bash
ssdeep test.txt
```

##### Хэширование `bamboo.exe` до изменения:
```bash
ssdeep bamboo.exe
```

##### Хэширование `bamboo.exe` после изменения:
```bash
ssdeep bamboo.exe
```
