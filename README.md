# giveDiscount

### Данный скрипт позволяет выставлять в автоматическом режиме скидку клиенту, если сумма сделок за месяц больше определенной суммы.

**Механизм работы**:
1. Создается сделка, заполняется сумма сделки.
2. При достижении определенного этапа, запускается бизнес-процесс в котором содержится вебхук по проверке сделок за последние 32 дня. Иными словами, скрипт начинает опрашивать успешные сделки за определенный промежуток времени и суммирует цены из данных сделок. 
3. Полученный результат сумм сделок передается в Бизнес-процесс через параметр. 
4. Внутри бизнес-процесса уже происходит или не происходит начисление скидки.

Решение может работать как на облачных, так и коробочных Битрикс24. 

**Как запустить**:
1. get_deal.php и auth.php необходимо разместить на хостинге с поддержкой SSL.
2. В разделе "Разработчикам" необходимо создать входящий вебхук с правами на CRM (crm) и Бизнес-процессы (bizproc). Подробнее как создать входящий / исходящий вебхук: [Ссылки на документацию 1С-Битрикс](https://github.com/thnik911/duplicate/blob/main/README.md#%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B8-%D0%BD%D0%B0-%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8E-1%D1%81-%D0%B1%D0%B8%D1%82%D1%80%D0%B8%D0%BA%D1%81).
3. Полученный "Вебхук для вызова rest api" прописать в auth.php.
4. В строке 91 скрипта get_deal.php в 'TEMPLATE_ID' необходимо указать ID бизнес-процесса, который необходимо запустить.
5. Делаем POST запрос посредством конструкции Webhook* через робот, или бизнес-процессом: https://yourdomain.com/path/get_deal.php?deal=123&cnt=456

**Переменные передаваемые в POST запросе:**

yourdomain.com - адрес сайта, на котором размещены скрипты auth.php и get_deal.php с поддержкой SSL.

path - путь до скрипта.

deal - ID сделки.

cnt - ID контакта, который связан со сделкой.

### Ссылки на документацию 1С-Битрикс 

<details><summary>Развернуть список</summary>

1. Действие Webhook внутри Бизнес-процесса / робота https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=57&LESSON_ID=8551
2. Как создать Webhook https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=99&LESSON_ID=8581&LESSON_PATH=8771.8583.8581

</details>

