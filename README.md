---
author: Lektion 7
date: MMMM dd, YYYY
paging: "%d / %d"
---

# Lektion 7

Hej och välkommen!

## Agenda

1. Frågor och repetition
2. Repetition av normalisering
3. Fortsättning projektbygge
4. Övning med handledning
5. Quiz frågor

---

# Normalisering

En samling med sätt, så kallade normalformer, att designa och strukturera tabeller för att uppnå integritet och förhindra data duplicering.

Normalformer: 1NF, 2NF & 3NF. Varje form har specifika regler att följa.

---

# Ett exempel utan normalisering

```sql
CREATE TABLE book_orders (
  isbn TEXT,
  title TEXT,
  author TEXT,
  author_email TEXT,
  customer_id INT,
  customer_name TEXT,
  date DATE,
  price DECIMAL
);
```

---

# Normalformer

## Första formen (1NF)

Varje rad och kolumn (cell) måste ha endast ett värde. En cell får inte innehålla en lista. "Listor" av saker hanteras genom relationer.

## Andra formen (2NF)

Tabell måste ha endast en primär nyckel, eller, tabell måste kolumner som alla är helt beroende av alla primära nycklar.

Följer inte 2NF: `student_id | student_name | course_id | course_name | course_description`

## Tredje formen (3NF)

Tabell får inte ha beroenden till kolumner (i andra tabeller) som inte är nycklar.

Följer inte 3NF: `patient_id | patient_name | doctor_number`

---

# Exempel utan normalisering

```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    date DATE,
    product_ids TEXT,
    product_amounts TEXT,
    product_descriptions TEXT,
    total_price DECIMAL(10, 2),
);
```

---

# Exempel med normalisering

```sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    date DATE,
);

CREATE TABLE order_items (
    order_id INT REFERENCES orders(id),
    product_id INT REFERENCES products(id),
    product_amount INT,
    PRIMARY KEY (order_id, product_id)
);

CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    description TEXT,
    price DECIMAL
);
```

---

# Gruppövning: implementera skapande av inlägg

Lägg till funktionalitet för att kunna skapa och spara inlägg. Försök att implementera det på ett OOP-sätt.

Alla grupper lämnar in sin kod efteråt så går vi igenom den tillsammans.

---

# Quiz frågor

- Varför behövs ofta två eller fler joins för Many-to-Many relationer?
- Du har följande tabeller
  - `id | player_name | player_goals`
  - `id | team_name | manager_id`
  - `team_id | player_id`
  - En kolumn skall läggas till: `player_shirt_number`, i vilken tabell ska den läggas till?
- Vad gör `ON DELETE RESTRICT`?
- Nämn ett exempel då `ON DELETE SET NULL` är passande.
- Varför är normalisering viktigt?
- Vad säger den första normalformen (1NF)?
- Vad säger den andra normalformen (2NF)?
- Vad säger den tredje normalformen (3NF)?
- Vilken constraint kan användas för att förhindra ändring av primary key?
- Varför följer inte tabellen normaliserings principer: `store_name | store_location | products`?
- Varför följer inte tabellen normaliserings principer: `patient_id | patient_name | doctor_number`?
