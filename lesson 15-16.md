### Поднятие контроллера домена (DC1) и настройка DHCP сервера

1. **Установка контроллера домена (DC1)** в отдельной подсети:
   - Разверните новую виртуальную машину (VM) с Windows Server в отдельной подсети (например, 10.10.0.0/24).
   - Установите роль Active Directory Domain Services (AD DS):
     ```bash
     Install-WindowsFeature -Name AD-Domain-Services
     ```
   - Настройте домен, например, `<фамилия>.tms (local)`:
     ```bash
     Install-ADDSForest -DomainName "<фамилия>.tms"
     ```
![image](https://github.com/user-attachments/assets/a01c22ee-bf9f-4390-a6b5-76f4e64f5185)


2. **Установка роли DHCP сервера в AD**:
   - Установите DHCP сервер:
     ```bash
     Install-WindowsFeature -Name DHCP -IncludeManagementTools
     ```
   - Откройте DHCP консоль и настройте диапазон IP-адресов для раздачи (например, от 192.168.10.100 до 192.168.10.200).
   - Укажите адрес DNS сервера, соответствующий вашему домену (например, 192.168.10.1).
   - Активируйте DHCP сервер:
     ```bash
     netsh dhcp server initiate reconcile
     ```

### Поднятие виртуальной машины Windows 10 и проверка DHCP

3. **Создание и настройка VM с Windows 10**:
   - Поднимите виртуальную машину с Windows 10 в той же подсети (192.168.10.0/24), в которой находится DC1.
   - Настройте сетевые параметры на VM для получения IP-адреса по DHCP.
   - После запуска, проверьте получение настроек через DHCP:
     ```bash
     ipconfig /all
     ```
   Убедитесь, что машина получила IP-адрес, шлюз и DNS-сервер от DHCP сервера.

4. **Добавление машины в домен**:
   - Откройте свойства системы на VM с Windows 10.
   - Выберите "Изменить параметры" и добавьте компьютер в домен `<фамилия>.tms`.
   - Перезагрузите компьютер для применения изменений.

![image](https://github.com/user-attachments/assets/d08ca4db-46b9-466c-b61e-1e17cc8e3ac3)

### Настройка GPO в Active Directory

5. **Создание организационного юнита (OU)**:
   - Откройте консоль управления Active Directory Users and Computers (ADUC).
   - Создайте новый OU с именем, например, `Company`.
   - Внутри `Company` создайте два организационных юнита: `fin` и `hr`.
   - Создайте двух пользователей в каждом из этих OU.

6. **Настройка GPO для OU `fin`**:
   - Откройте "Group Policy Management".
   - Создайте новый GPO с именем `fin_gpo`.
   - Примените следующие настройки для паролей:
     - Минимальная длина пароля: 10 символов.
     - Помнить предыдущие 5 паролей.
     - Срок действия пароля: 90 дней.
     - Эти настройки находятся в разделе **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy**.
   - Примените этот GPO к OU `fin`.
   - ![image](https://github.com/user-attachments/assets/99595f9f-2f2d-499d-beae-a8139336d636)


7. **Настройка GPO для OU `hr`**:
   - Создайте новый GPO с именем `hr_gpo`.
   - Примените следующие настройки:
     - Минимальная длина пароля: 8 символов.
     - Срок действия пароля: 180 дней.
     - Блокировка экрана после 15 минут бездействия.
     - Эти настройки можно найти в **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy** (для паролей) и **User Configuration > Administrative Templates > Control Panel > Personalization** (для блокировки экрана).
   - Примените GPO к OU `hr`.
   - ![image](https://github.com/user-attachments/assets/8e6a2a09-11fc-46f1-9abd-1550dd717717)


### Проверка применения групповых политик на VM с Windows 10

8. **Проверка GPO через PowerShell**:
   - Зайдите под одним из созданных пользователей на VM с Windows 10.
   - Откройте PowerShell и выполните команду для проверки примененных политик:
     ```bash
     gpresult /r
     ```
 ![image](https://github.com/user-attachments/assets/7eab2112-0df0-4689-86a2-84f88d78c4c8)


