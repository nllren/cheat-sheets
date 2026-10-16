# SQL — HAVING Cheat Sheet

## 1. `HAVING` — фильтрация групп

`HAVING` фильтрует группы после выполнения `GROUP BY`. Позволяет использовать агрегатные функции в условии.

```sql
SELECT home_type, AVG(price) AS avg_price
FROM Rooms
GROUP BY home_type
HAVING avg_price > 50;
```

Выведет типы жилья, у которых средняя цена больше 50.

## 2. `WHERE` vs `HAVING`

| Оператор | Что фильтрует | Когда выполняется |
|---|---|---|
| `WHERE` | Отдельные строки | До группировки |
| `HAVING` | Группы | После группировки |

```sql
-- Сначала отбираем строки, затем группируем
SELECT home_type, AVG(price) AS avg_price
FROM Rooms
WHERE price > 50
GROUP BY home_type;
```

```sql
-- Сначала группируем, затем отбираем группы
SELECT home_type, AVG(price) AS avg_price
FROM Rooms
GROUP BY home_type
HAVING AVG(price) > 50;
```

**Важно:** `WHERE` фильтрует строки до вычисления агрегатов, а `HAVING` — результаты группировки.

## 3. Порядок запроса

```sql
SELECT столбцы
FROM таблица
WHERE условие_для_строк
GROUP BY столбец_группировки
HAVING условие_для_групп
ORDER BY столбец_сортировки;
```

Логический порядок выполнения:

1. `FROM` — выбирает таблицу.
2. `WHERE` — фильтрует строки.
3. `GROUP BY` — формирует группы.
4. `HAVING` — фильтрует группы.
5. `SELECT` — формирует результат.
6. `ORDER BY` — сортирует результат.

## 4. Пример с несколькими условиями

Найти типы жилья с телевизором, у которых минимум 5 помещений, и вывести минимальную цену:

```sql
SELECT home_type, MIN(price) AS min_price
FROM Rooms
WHERE has_tv = TRUE
GROUP BY home_type
HAVING COUNT(*) >= 5;
```

- `WHERE has_tv = TRUE` — выбирает помещения с телевизором.
- `GROUP BY home_type` — группирует их по типу.
- `HAVING COUNT(*) >= 5` — оставляет группы минимум с 5 помещениями.
- `MIN(price)` — находит минимальную цену в каждой группе.

## 5. Кратко

- `WHERE` — фильтрация строк.
- `GROUP BY` — группировка строк.
- `HAVING` — фильтрация групп.
- `COUNT(*)`, `AVG()`, `SUM()`, `MIN()`, `MAX()` можно использовать в `HAVING`.
- Для фильтрации по результату агрегатной функции используй `HAVING`, а не `WHERE`.
