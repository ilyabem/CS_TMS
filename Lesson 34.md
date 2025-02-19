Найти препода в архивах социальных сетей

Алексей Смирнов 8 октября 1988 года

Номер телефона +375 44 514 1228

Tg - @sm1love

X - https://x.com/AISmirnoff

Личный сайт https://thevopz.com/elements.html#

in - https://www.linkedin.com/in/sm1lex/

CodeWars https://www.codewars.com/users/Aleksey%20Smirnov/stats (???)

gmail smilovesmirnov@gmail.com

2.	Произвести OSINT на организацию либо компанию
с помощью theHarvester

●	Выполнить запросы на получение записей домена.

●	Поискать поддомены сайта

●	На сайте найти электронную почту сотрудника, выполнить поиск дополнительных записей электронных почт

●	Найти имя и фамилию или номер телефона на сайте и постараться найти о нем информацию

`theHarvester` — это мощный инструмент для сбора информации с открытых источников (OSINT), и с его помощью можно узнать множество данных о домене или компании. Вот что еще вы можете извлечь с помощью `theHarvester`:

1. **Поиск субдоменов**:
   - Используя опцию `-d`, вы можете искать субдомены для заданного домена. Это полезно для выявления скрытых сервисов и ресурсов компании.
   - Пример: `theHarvester.py -d example.com -b bing`
![photo_2024-12-07_17-34-45](https://github.com/user-attachments/assets/0cbbcdff-0ee8-4923-bc11-775ee18d38ef)

2. **Поиск IP-адресов**:
   - Если домен имеет публично доступные IP-адреса, `theHarvester` может их найти через различные источники (например, Shodan, Censys).
   - Пример: `theHarvester.py -d example.com -b shodan`

3. **Проверка на уязвимости**:
   - Вы можете проверить, есть ли возможности для захвата домена (например, атаки на незащищенные субдомены). Это можно сделать с помощью флага `-t` (опция для проверки захвата).
   - Пример: `theHarvester.py -d example.com -t`

4. **Поиск e-mail адресов**:
   - `theHarvester` может собирать e-mail адреса, которые могут быть связаны с определенным доменом.
   - Пример: `theHarvester.py -d example.com -b google`
![photo_2024-12-07_17-38-40](https://github.com/user-attachments/assets/5ed2a894-c4ad-4d71-8a41-be77f0dcac88)

5. **Поиск информации по социальной инженерии**:
   - Вы можете настроить инструмент для поиска данных, которые могут быть полезны для социальной инженерии, например, через исследование информации в социальных сетях или через другие открытые источники.
   - Пример: `theHarvester.py -d example.com -b github-code`

6. **Поиск хостов**:
   - Вы можете искать хосты, которые могут быть связаны с доменом, включая субдомены, и использовать полученную информацию для проведения более глубокого анализа.
   - Пример: `theHarvester.py -d example.com -b binaryedge`

7. **DNS-резолвинг**:
   - Если вы хотите проверить DNS-результаты для субдоменов, используйте флаг `-n`. Это позволит вам выполнить запросы к DNS-серверам для разрешения имен.
   - Пример: `theHarvester.py -d example.com -n`

8. **Ограничение количества результатов**:
   - Вы можете ограничить количество выводимых результатов с помощью опции `-l`. Это полезно для фокусировки на наиболее значимых данных.
   - Пример: `theHarvester.py -d example.com -l 100`

9. **Генерация отчетов**:
   - С помощью флага `-f` вы можете сохранять результаты в файлы в формате XML или JSON. Это удобно для дальнейшей обработки данных или отчетности.
   - Пример: `theHarvester.py -d example.com -f results.xml`

10. **Использование прокси-серверов**:
    - В случае необходимости, вы можете настроить использование прокси для анонимизации запросов или обхода блокировок.
    - Пример: `theHarvester.py -d example.com -p`

11. **Поиск по различным источникам**:
    - `theHarvester` поддерживает множество источников для поиска, таких как:
      - `google`, `bing`, `duckduckgo`, `shodan`, `crtsh`, `securitytrails`, `virustotal` и многие другие.
    - Вы можете комбинировать их для более точных или расширенных поисков.
    - Пример: `theHarvester.py -d example.com -b bing -b google`


Почта главного редактора Андрея Гомыляева — ga@onliner.by.

in - https://www.linkedin.com/in/%D0%B0%D0%BD%D0%B4%D1%80%D0%B5%D0%B9-%D0%B3%D0%BE%D0%BC%D1%8B%D0%BB%D1%8F%D0%B5%D0%B2-226150221/?originalSubdomain=by

