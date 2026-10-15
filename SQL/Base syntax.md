# 📘 SQL — базовый синтаксис

## 1. Вывод значений

```sql
SELECT 'Hello world';
SELECT 42;
```

## 2. Все столбцы таблицы

```sql
SELECT * FROM FamilyMembers;
```

`*` — все столбцы.

## 3. Выбор конкретных столбцов

```sql
SELECT member_id, member_name
FROM FamilyMembers;
```

Несколько столбцов разделяются запятой.

## 4. Псевдонимы (`AS`)

```sql
SELECT member_name AS Name
FROM FamilyMembers;
```

Можно и без `AS`:

```sql
SELECT member_name Name
FROM FamilyMembers;
```

`AS` — задаёт новое имя столбца в результате.

---

## ⚡ Запомнить

| Оператор | Назначение |
|---|---|
| `SELECT` | Выбрать данные |
| `*` | Все столбцы |
| `FROM` | Из какой таблицы |
| `AS` | Псевдоним столбца |
| `,` | Разделитель столбцов |
| `;` | Конец запроса |

### 🧩 Шаблон

```sql
SELECT столбцы
FROM таблица;
```
