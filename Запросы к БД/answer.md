# Ответы

Я сгенерировала данные для таблиц с помощью Python (в файле <a href="https://github.com/tashacraft/test_tasks/blob/main/%D0%97%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D1%8B%20%D0%BA%20%D0%91%D0%94/create_data.ipynb">create_data.ypynb</a>):

Таблица Users - возраст от 18 до 80 лет, всего 300 записей

Таблица Purchases:
- даты от 01.01.2022 до 31.12.2022
- id товара (200 разных id)
- всего 1000 записей

Таблица Items - цены от 10 до 500 руб, всего 200 записей

1. Какую сумму в среднем в месяц тратит пользователь в возрастном диапазоне от 18 до 25 лет включительно?

```
SELECT avg(avg_order) AS avg_order_18_25
FROM (
    SELECT month,
        avg(sum_user) AS avg_order
    FROM (
      select (date_trunc('month', CAST(date AS date))):: date as month,
          u.userid,
          sum(price) AS sum_user
      from users AS u
      JOIN purchases AS pu ON u.userid = pu.userid
      JOIN items AS i ON pu.itemid=i.itemid
      WHERE 
              age >= 18
          AND 
              age <= 25
      GROUP BY date_trunc('month', CAST(date AS date)), u.userid
      ) AS sum_user_month
     GROUP BY month
 ) AS avg_order_user_month
```

2. Какую сумму в среднем в месяц тратит пользователь в возрастном диапазоне от 26 до 35 лет включительно?

```
SELECT avg(avg_order) AS avg_order_26_35
FROM (
    SELECT month,
        avg(sum_user) AS avg_order
    FROM (
      SELECT (date_trunc('month', CAST(date AS date))):: date as month,
          u.userid,
          sum(price) AS sum_user
      FROM users AS u
      JOIN purchases AS pu ON u.userid = pu.userid
      JOIN items AS i ON pu.itemid=i.itemid
      WHERE 
              age >= 26
          AND 
              age <= 35
      GROUP BY date_trunc('month', CAST(date AS date)), u.userid
      ) AS sum_user_month
     GROUP BY month
 ) AS avg_order_user_month;
```

3. В каком месяце года выручка от пользователей в возрастном диапазоне 35+ самая большая?

```
SELECT 
	extract(month from CAST(date AS date)) AS month_order,
	sum(price) AS sum_month
FROM users AS u
JOIN purchases AS pu ON u.userid = pu.userid
JOIN items AS i ON pu.itemid=i.itemid
WHERE age >= 35 
GROUP BY extract(month from CAST(date AS date))
ORDER By sum_month DESC;
```

4. Какой товар дает наибольший вклад в выручку за последний год?

```
SELECT i.itemid,
	sum(price) AS sum_year
FROM items AS i
JOIN purchases AS pu ON pu.itemid=i.itemid
WHERE CAST(date AS date) BETWEEN '2022-01-01' AND '2022-12-31'
GROUP BY i.itemid
ORDER BY sum_year DESC;
```

5. Топ-3 товаров по выручке и их доля в общей выручке за любой год.

```
SELECT 
	itemid,
	sum_year,
	(sum_year / sum(sum_year) OVER ()) * 100 AS percent_item
FROM (
  SELECT i.itemid AS itemid,
      SUM(price) AS sum_year
  FROM items AS i 
  JOIN purchases AS pu ON pu.itemid=i.itemid
  WHERE CAST(date AS date) BETWEEN '2022-01-01' AND '2022-12-31'
  GROUP BY i.itemid
  ORDER BY sum_year DESC
  ) AS sum_y
LIMIT 3;
```


```python

```
