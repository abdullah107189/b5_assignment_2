# PostgreSQL Importent Questions

### 1: PostgreSQL কী?

**উত্তর:**
PostgreSQL একটি **ওপেন-সোর্স রিলেশনাল ডেটাবেইস ম্যানেজমেন্ট সিস্টেম (RDBMS)**। এটি SQL (Structured Query Language) এবং আধুনিক অ্যাপ্লিকেশনের জন্য অনেক উন্নত ফিচার যেমন: JSON, Arrays, Window Functions, CTE, এবং Stored Procedures সমর্থন করে।

**মূল বৈশিষ্ট্য:**

* ACID কমপ্লায়েন্ট (যেটা ডেটার নিরাপত্তা ও স্থায়িত্ব নিশ্চিত করে)
* Multi-version Concurrency Control (MVCC)
* Open-source এবং community-driven
* Custom functions তৈরি করা যায় (PL/pgSQL)

**ব্যবহার কোথায় হয়?**

* Web Applications
* Data Analytics Systems
* Enterprise Software

---

### 2: PostgreSQL-এ Schema এর উদ্দেশ্য কী?

**উত্তর:**
Schema হচ্ছে PostgreSQL ডেটাবেইসের ভেতরে একটি **লজিক্যাল কন্টেইনার**, যেখানে আমরা টেবিল, ভিউ, ফাংশন ইত্যাদি সংগঠিতভাবে রাখতে পারি। এটি একধরনের "ফোল্ডার" এর মতো, যাতে একই ডেটাবেইসে একাধিক স্কিমা রাখা যায়।

**উদাহরণ:**
একটি `company_db` ডেটাবেইসে:

* `hr` schema → Employees, Leaves
* `sales` schema → Orders, Customers

**লাভ কী?**

* নামের সংঘর্ষ এড়ানো যায়
* অ্যাক্সেস কন্ট্রোল সহজ হয় (user-wise schema)
* বড় প্রজেক্টে module ভিত্তিক ডেটা ম্যানেজমেন্ট সহজ হয়

---

### 3: Primary Key ও Foreign Key এর পার্থক্য কী?

**Primary Key:**

* টেবিলের প্রতিটি রেকর্ডকে ইউনিকভাবে চিহ্নিত করে
* NULL থাকতে পারে না
* একটি টেবিলে একটির বেশি Primary Key থাকতে পারে না

**Foreign Key:**

* অন্য টেবিলের Primary Key এর সাথে সংযুক্ত
* Referential Integrity বজায় রাখে
* একই টেবিলে একাধিক Foreign Key থাকতে পারে

**উদাহরণ:**

```sql
-- Parent Table
CREATE TABLE departments (
  dept_id SERIAL PRIMARY KEY,
  name VARCHAR(100)
);

-- Child Table
CREATE TABLE employees (
  emp_id SERIAL PRIMARY KEY,
  dept_id INT REFERENCES departments(dept_id),
  name VARCHAR(100)
);
```

---

### 4: VARCHAR ও CHAR এর মধ্যে পার্থক্য কী?

| বৈশিষ্ট্য           | VARCHAR        | CHAR              |
| ------------------- | -------------- | ----------------- |
| দৈর্ঘ্য পরিবর্তনশীল | হ্যাঁ          | না (Fixed length) |
| Performance         | তুলনামূলক ভালো | ধীর হতে পারে      |
| Trailing Spaces     | Remove করে     | রাখতে পারে        |

**কখন কোনটা ব্যবহার করবো?**

* `VARCHAR` যখন ভিন্ন ভিন্ন দৈর্ঘ্যের text (e.g. নাম, ঠিকানা)
* `CHAR(1)` যখন Fixed size দরকার (e.g. gender = 'M'/'F')

---

### 5: SELECT স্টেটমেন্টে WHERE clause এর কাজ কী?

**উত্তর:**
`WHERE` clause ব্যবহার করা হয় **ডেটা ফিল্টার করার জন্য**। এটি SELECT, UPDATE, DELETE স্টেটমেন্টের সাথে নির্দিষ্ট শর্ত অনুযায়ী রেকর্ড খুঁজে বের করতে সাহায্য করে।

**উদাহরণ:**

```sql
SELECT *
FROM rangers
WHERE region = 'Northern Hills';
```

এই কোয়েরি শুধু সেই রেঞ্জারদের দেখাবে যাদের region হলো 'Northern Hills'।

**কাজের ধরন:**

* তুলনা: `=`, `!=`, `<`, `>`
* লজিক্যাল: `AND`, `OR`, `NOT`
* প্যাটার্ন: `LIKE`, `ILIKE`
* NULL চেক: `IS NULL`, `IS NOT NULL`

---

Prepared by: Md. Abdullah All Shamem
Assignment: Wildlife Conservation PostgreSQL Assignment
Date: June 2025
