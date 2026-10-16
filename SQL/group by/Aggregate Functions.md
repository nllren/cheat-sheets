# SQL — Aggregate Functions Cheat Sheet

## 1. Агрегатные функции

Агрегатные функции выполняют вычисления по набору значений и возвращают одно значение. Используются с `GROUP BY` или без него.

| Функция | Назначение |
|---|---|
| `COUNT(*)` | Количество строк |
| `COUNT(column)` | Количество значений, не равных `NULL` |
| `SUM(column)` | Сумма значений |
| `AVG(column)` | Среднее значение |
| `MIN(column)` | Минимальное значение |
| `MAX(column)` | Максимальное значение |

## 2. Примеры

**Количество строк в таблице:**

```sql
SELECT COUNT(*) AS amount
FROM Rooms;
```

**Средняя цена по типу жилья:**

```sql
SELECT home_type, AVG(price) AS avg_price
FROM Rooms
GROUP BY home_type;
```

**Количество объектов каждого типа, от большего к меньшему:**

```sql
SELECT home_type, COUNT(*) AS amount
FROM Rooms
GROUP BY home_type
ORDER BY amount DESC;
```

**Самая поздняя дата выезда для каждого помещения:**

```sql
SELECT room_id, MAX(end_date) AS last_end_date
FROM Reservations
GROUP BY room_id;
```

## 3. Важные правила

- Все агрегатные функции, кроме `COUNT(*)`, игнорируют значения `NULL`.
- `COUNT(*)` считает все строки, включая строки с `NULL`.
- Без `GROUP BY` агрегатная функция вычисляется по всему набору строк.
- С `GROUP BY` функция вычисляется отдельно для каждой группы.
- Результат можно переименовать с помощью `AS`.

## Кратко

```sql
SELECT group_column,
       COUNT(*) AS amount,
       AVG(price) AS avg_price,
       MIN(price) AS min_price,
       MAX(price) AS max_price,
       SUM(price) AS total_price
FROM Rooms
GROUP BY group_column
ORDER BY amount DESC;
```

