# SQL — IS NULL, BETWEEN, IN Cheat Sheet

## 1. `IS NULL` — проверка на отсутствие значения

```sql
-- Значение отсутствует
SELECT * FROM Teacher
WHERE middle_name IS NULL;

-- Значение присутствует
SELECT * FROM Teacher
WHERE middle_name IS NOT NULL;
```

**Важно:** для проверки `NULL` используй `IS NULL` или `IS NOT NULL`, а не `= NULL`.

## 2. `BETWEEN` — проверка диапазона

```sql
SELECT * FROM Payments
WHERE unit_price BETWEEN 100 AND 500;
```

- Включает обе границы: `100` и `500`.
- Эквивалентно условию:

```sql
WHERE unit_price >= 100 AND unit_price <= 500
```

## 3. `IN` — проверка по списку значений

```sql
SELECT * FROM FamilyMembers
WHERE status IN ('father', 'mother');
```

Выбирает строки, где значение входит в указанный список.

Отрицание — `NOT IN`:

```sql
SELECT * FROM FamilyMembers
WHERE status NOT IN ('father', 'mother');
```

## Кратко

| Оператор | Для чего | Пример |
|---|---|---|
| `IS NULL` | Значение отсутствует | `WHERE name IS NULL` |
| `IS NOT NULL` | Значение присутствует | `WHERE name IS NOT NULL` |
| `BETWEEN` | Значение в диапазоне включительно | `WHERE age BETWEEN 18 AND 30` |
| `IN` | Значение входит в список | `WHERE status IN ('A', 'B')` |
| `NOT IN` | Значение не входит в список | `WHERE status NOT IN ('A', 'B')` |
