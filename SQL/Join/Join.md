# SQL — JOIN Cheat Sheet

## 1. `JOIN` — объединение таблиц

`JOIN` позволяет получать данные из нескольких таблиц, связывая строки по заданному условию.

```sql
SELECT столбцы
FROM таблица_1
INNER JOIN таблица_2
    ON таблица_1.id = таблица_2.id;
```

- `ON` — условие соединения таблиц.
- `таблица.столбец` — обращение к конкретному столбцу таблицы.

## 2. Основные виды JOIN

| Оператор | Что возвращает |
|---|---|
| `INNER JOIN` | Только строки, для которых найдены совпадения в обеих таблицах |
| `LEFT JOIN` | Все строки левой таблицы и совпадения из правой; если совпадения нет — `NULL` |
| `RIGHT JOIN` | Все строки правой таблицы и совпадения из левой; если совпадения нет — `NULL` |
| `FULL OUTER JOIN` | Все строки обеих таблиц, включая строки без совпадений |

`INNER JOIN` можно записать просто как `JOIN`. В MySQL `FULL OUTER JOIN` напрямую не поддерживается.

## 3. Пример `INNER JOIN`

Получить имена членов семьи и стоимость покупок:

```sql
SELECT
    p.family_member,
    fm.member_name,
    p.amount * p.unit_price AS price
FROM Payments AS p
INNER JOIN FamilyMembers AS fm
    ON p.family_member = fm.member_id;
```

Таблицы соединяются по условию `p.family_member = fm.member_id`.

## 4. Выбор столбцов

```sql
-- Все столбцы обеих таблиц
SELECT *
FROM Payments AS p
JOIN FamilyMembers AS fm
    ON p.family_member = fm.member_id;

-- Все столбцы только FamilyMembers
SELECT fm.*
FROM Payments AS p
JOIN FamilyMembers AS fm
    ON p.family_member = fm.member_id;

-- Отдельные столбцы и все поля другой таблицы
SELECT p.payment_id, p.family_member, fm.*
FROM Payments AS p
JOIN FamilyMembers AS fm
    ON p.family_member = fm.member_id;
```

## 5. Псевдонимы таблиц

Псевдонимы сокращают названия таблиц и делают запросы удобнее.

```sql
SELECT pass.id, pass.name
FROM Passenger AS pass
JOIN Pass_in_trip AS pit
    ON pit.passenger = pass.id;
```

- `Passenger AS pass` — псевдоним `pass`.
- `Pass_in_trip AS pit` — псевдоним `pit`.
- `AS` можно опустить: `Passenger pass`.
- После назначения псевдонима используй его вместо исходного имени таблицы.

## 6. Важные правила

- `ON` задаёт условие, по которому сопоставляются строки.
- Если столбец есть в нескольких таблицах, указывай его вместе с именем таблицы или псевдонимом: `p.id`.
- `*` выводит все столбцы всех таблиц в `FROM`.
- Для соединения нескольких таблиц добавляй отдельный `JOIN ... ON` для каждой.
- Если одна строка одной таблицы совпадает с несколькими строками другой, результат может содержать несколько строк для этой записи.

## Шаблон

```sql
SELECT a.column1, b.column2
FROM TableA AS a
INNER JOIN TableB AS b
    ON a.id = b.table_a_id;
```
