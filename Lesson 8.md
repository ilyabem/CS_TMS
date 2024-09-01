
### 1. Установите Docker на виртуальную машину Ubuntu

Если Docker еще не установлен на вашей виртуальной машине, следуйте этим шагам:

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
```

### 2. Запустите Docker контейнер Juice Shop

Скачайте и запустите Docker контейнер Juice Shop:

```bash
docker run -d -p 3000:80 bkimminich/juice-shop
```

Эта команда загрузит и запустит Juice Shop на порту 80 вашей виртуальной машины.
Для запуска Juice Shop в браузере необходимо прописать `localhost:80`


![image](https://github.com/user-attachments/assets/7fa631a4-6228-4377-a5bc-e8cffc19afc0)

### 3. Установите необходимые пакеты для компиляции XerXes

Вам нужно будет установить компилятор `gcc`, если он еще не установлен:

```bash
sudo apt update
sudo apt install -y gcc unzip
```

### 4. Распакуйте архив XerXes

Предполагая, что вы уже скачали ZIP архив XerXes на вашу виртуальную машину, распакуйте его:

```bash
unzip xerxes.zip -d xerxes
cd xerxes
```

### 5. Скомпилируйте XerXes

Теперь, когда вы находитесь в директории XerXes, скомпилируйте его с помощью `gcc`:

```bash
gcc xerxes.c -o xerxes
```

### 6. Проведите DOS атаку на Juice Shop

Теперь вы можете запустить атаку на Juice Shop. Используйте IP-адрес или имя хоста вашей виртуальной машины и порт 80:

```bash
./xerxes 127.0.0.1 80
```

![image](https://github.com/user-attachments/assets/6e773391-d659-4051-8f3f-26f274e8cd16)


Замените `127.0.0.1` на реальный IP-адрес, если Juice Shop работает не на локальном хосте.

### 7. Посмотрите на нагрузку на контейнер Juice Shop

Чтобы наблюдать за нагрузкой, вызванной атакой, вы можете использовать команду `top` в новом терминале:

```bash
top
```

Чтобы фильтровать процессы, связанные с Docker, нажмите `o` и введите:

```
COMMAND=docker
```

Это покажет только процессы Docker. Вы увидите нагрузку на процессор и память, что укажет на влияние DOS-атаки на контейнер Juice Shop.
![image](https://github.com/user-attachments/assets/64de187a-2e05-49ad-beb5-9af854b8b866)

Максимальная нагрузка, которую получилось достичь - 40% , но в среднем нагрузка 10-15% 

# Проводите DOS атаку на сервисы только при наличии полного официального разрешения. 
<s>P.S будешь проводить без разрешения - получишь по жопе</s> 
