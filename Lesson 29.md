### Условия для проверки пароля:
1. Длина пароля должна быть 8 символов или больше.
2. Пароль обязан включать хотя бы одну букву в верхнем регистре.
3. Также требуется хотя бы одна буква в нижнем регистре.
4. Необходимо наличие хотя бы одной цифры.
5. Пароль должен содержать хотя бы один специальный символ (`@, #, $, %, &, *, !` и т.д.).

---

### Пример скрипта на **Bash**
```bash
#!/bin/bash

check_password() {
    local pwd="$1"
    local min_length=8
    local special_chars='[@#$%&*!]'

    if [[ ${#pwd} -lt $min_length ]]; then
        echo "Ошибка: пароль слишком короткий. Минимум: $min_length символов."
        return 1
    fi

    if [[ ! $pwd =~ [A-Z] ]]; then
        echo "Ошибка: в пароле должна быть хотя бы одна заглавная буква."
        return 1
    fi

    if [[ ! $pwd =~ [a-z] ]]; then
        echo "Ошибка: в пароле должна быть хотя бы одна строчная буква."
        return 1
    fi

    if [[ ! $pwd =~ [0-9] ]]; then
        echo "Ошибка: в пароле должна быть хотя бы одна цифра."
        return 1
    fi

    if [[ ! $pwd =~ $special_chars ]]; then
        echo "Ошибка: пароль должен содержать хотя бы один из символов: @#$%&*!"
        return 1
    fi

    echo "Пароль успешно прошел проверку."
    return 0
}

read -s -p "Введите пароль для проверки: " pwd
echo
check_password "$pwd"
```

---

### Пример скрипта на **Python**
```python
import re

def check_password(password):
    min_length = 8
    if len(password) < min_length:
        return f"Ошибка: пароль короче {min_length} символов."
    if not re.search(r'[A-Z]', password):
        return "Ошибка: отсутствует хотя бы одна буква в верхнем регистре."
    if not re.search(r'[a-z]', password):
        return "Ошибка: отсутствует хотя бы одна буква в нижнем регистре."
    if not re.search(r'[0-9]', password):
        return "Ошибка: отсутствует хотя бы одна цифра."
    if not re.search(r'[@#$%&*!]', password):
        return "Ошибка: должен быть хотя бы один специальный символ (@#$%&*!)."
    return "Пароль соответствует требованиям."

password = input("Введите пароль для проверки: ")
result = check_password(password)
print(result)
```

---
Инструкция

---

### Использование скрипта на **Bash**:
1. **Создайте файл** для скрипта:
   ```bash
   nano validate_password.sh
   ```
2. **Скопируйте код** из раздела Bash в созданный файл и сохраните его.
3. **Сделайте скрипт исполняемым**:
   ```bash
   chmod +x validate_password.sh
   ```
4. **Запустите скрипт**:
   ```bash
   ./validate_password.sh
   ```
5. Введите пароль, когда скрипт запросит его (пароль будет скрыт). После этого вы увидите результат проверки.

---

### Использование скрипта на **Python**:
1. **Создайте файл** с кодом Python:
   ```bash
   nano validate_password.py
   ```
2. **Скопируйте код** из раздела Python в файл и сохраните его.
3. Убедитесь, что Python установлен. Чтобы проверить, выполните:
   ```bash
   python3 --version
   ```
4. **Запустите скрипт**:
   ```bash
   python3 validate_password.py
   ```
5. Когда скрипт попросит ввести пароль, напечатайте его (символы будут видны) и нажмите Enter. Результат проверки появится на экране.

---

### Пример работы:
1. **Для Bash**:
   ```bash
   Введите пароль для проверки: 
   # если пароль `Passw@rd1`
   Пароль успешно прошел проверку.
   # если пароль `password`
   Ошибка: в пароле должна быть хотя бы одна заглавная буква.
   ```

2. **Для Python**:
   ```bash
   Введите пароль для проверки: Passw@rd1
   Пароль соответствует требованиям.

   Введите пароль для проверки: password
   Ошибка: отсутствует хотя бы одна буква в верхнем регистре.
