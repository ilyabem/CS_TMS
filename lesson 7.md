# 1. Изучить SQL запросы.
   5 заданий готово)
   ![t1](https://github.com/user-attachments/assets/21890bfc-47c5-4c5a-9b62-af031f3f1eb2)
# 2. Лабораторные работы по OWASP TOP 10.
  ## Выполнить 2 лабораторные работы из практики Brocken Access Control
  Но прежде чем начать выполнять лабораторные работы, необходимо установить ` Burp Suite professional `.
Т.к любой кряк это Backdoor мы будем вешать этот инструмент на виртуальную машину.
Инструкция по установке на Kali будет по ссылке ниже.
https://medium.com/@Kaizen2977/install-burp-suite-pro-free-on-linux-31aa30f0335c 

После установки и попытки открыть в программе burp suite браузер может возникнуть ошибка:


` net.portswigger.devtools.client.q: Refusing to start browser as your current configuretion does not support running without sandbox `


Эта ошибка возникает из-за того, что браузер, встроенный в Burp Suite, требует запуска в режиме ` sandboх ` для обеспечения безопасности.
Чтоб решить эту проблему необходимо запускать burp suite не от имени root-пользователя. Но если и это не помогло , тогда нужно покопаться с изменением прав доступа к этому файлу ` crome-sandbox `. 
Для этого в терминале нужно прописать команду: 


` sudo find /Documents/Burp -name chrome-sandbox -exec chown root:root {} \; -exec chmod 4755 {} \; `
только путь поменять не забудь. `
### Lab Broken Access Controll 1

![таска 2 лаба 1](https://github.com/user-attachments/assets/55a72085-c532-42ba-959a-82661269d7e2)

### Lab Broken Access Controll_2
![image](https://github.com/user-attachments/assets/6658b93e-4be8-4dbe-bdaa-b90f3e342ae0)



## Выполнить 1 лабораторную работу из практики Injections
### Lab Injection 1
![image](https://github.com/user-attachments/assets/8ff8eb15-36a0-40ed-be0b-ccb49b12f78e)

## Выполнить 1 лабораторную работу из практики Server-Side Request Forgery
### Lab SSRF 1
![image](https://github.com/user-attachments/assets/e968808d-f179-49d0-abfa-9f47f38ce3e2)


