# Тестовое задание на SQL-запросы

<b>Дано</b>

У вас SQL база с таблицами:
1) Users(userId, age)
2) Purchases (purchaseId, userId, itemId, date)
3) Items (itemId, price).

<b>Ответы в файле <a href="https://github.com/tashacraft/test_tasks/blob/main/%D0%97%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D1%8B%20%D0%BA%20%D0%91%D0%94/answer.md">answer.md</a></b>

<b>Генерация данных для таблиц в файле <a href="https://github.com/tashacraft/test_tasks/blob/main/%D0%97%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D1%8B%20%D0%BA%20%D0%91%D0%94/create_data.ipynb">create_data.ipynb</a></b>

<b>Задачи</b>

Напишите SQL запросы для расчета следующих метрик:

1. какую сумму в среднем в месяц тратит:
- пользователи в возрастном диапазоне от 18 до 25 лет включительно
- пользователи в возрастном диапазоне от 26 до 35 лет включительно

2. в каком месяце года выручка от пользователей в возрастном диапазоне 35+ самая большая
3. какой товар обеспечивает дает наибольший вклад в выручку за последний год
4. топ-3 товаров по выручке и их доля в общей выручке за любой год

Будет здорово, если ваше решение оформлено в виде работающего кода и основательно протестировано на придуманных данных (код для наполнения данными тоже приложите).
Для тестирования можно использовать онлайн-редактор https://sqliteonline.com/
Предпочтительный диалект - PostgreSQL, но можете использовать любой из доступных.

