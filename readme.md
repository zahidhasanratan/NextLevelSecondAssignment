## 1, What is PostgreSQL?

উত্তর:
PostgreSQL হল একটা ডেটাবেজ ম্যানেজমেন্ট সিস্টেম, যেটা দিয়ে আমরা বিভিন্ন রকম তথ্য সাজিয়ে রাখতে পারি। ধরেন, আপনি একটা স্কুলের ছাত্রদের নাম, ক্লাস, ভর্তি হওয়ার তারিখ রাখতে চান — এই রকম কাজগুলো করার জন্যই PostgreSQL খুব কাজের।

এটা একটা ফ্রি ও ওপেন সোর্স সফটওয়্যার, মানে যেকেউ ব্যবহার করতে পারে, কোনো টাকা-পয়সা লাগে না। ছোট প্রজেক্ট হোক বা বড় কর্পোরেট লেভেলের সিস্টেম, সবখানেই PostgreSQL ব্যবহার করা যায়।

PostgreSQL এর কিছু ভালো দিক
SQL দিয়ে সহজেই জটিল জিনিস খুঁজে বের করা যায়।

অনেক ইউজার একসাথে কাজ করলেও সমস্যা হয় না।

JSON টাইপের ডেটাও সাপোর্ট করে — মানে শুধু টেবিল না, একটু জটিল গঠনও রাখা যায়।

খুব নিরাপদ আর ডেটা লসের ঝুঁকি কম।

একটা ছোট্ট উদাহরণ
```sql
CREATE TABLE students (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  class INTEGER,
  admission_date DATE
);
```
এখানে একটা students নামে টেবিল বানানো হয়েছে, যেখানে প্রতিটা ছাত্রের নাম, ক্লাস, আর ভর্তি হওয়ার তারিখ রাখা যাবে। id হচ্ছে আলাদা করে চেনার জন্য একটা ইউনিক আইডি।

## 1, Explain the Primary Key and Foreign Key concepts in PostgreSQL
PostgreSQL-এ ডেটাবেজ ডিজাইন করতে গেলে Primary Key এবং Foreign Key—এই দুইটা জিনিস খুবই গুরুত্বপূর্ণ। এদের সাহায্যে আমরা ডেটাগুলোর মধ্যে সম্পর্ক তৈরি করতে পারি এবং ডেটাবেজকে সুশৃঙ্খল ও নির্ভরযোগ্য রাখতে পারি।

Primary Key কী?
Primary Key হল এমন একটা কলাম (বা একাধিক কলামের সমন্বয়), যা টেবিলের প্রতিটি রেকর্ডকে ইউনিক (অদ্বিতীয়) করে তোলে। অর্থাৎ, যেই ফিল্ডকে Primary Key বানানো হয়, সেখানে কখনোই ডুপ্লিকেট ভ্যালু বা NULL ভ্যালু থাকতে পারে না।

⭐ মূল বৈশিষ্ট্য:
প্রতিটা রেকর্ডের জন্য ইউনিক আইডেন্টিফায়ার তৈরি করে

NULL ভ্যালু রাখা যায় না

এক টেবিলে শুধুমাত্র একটি Primary Key থাকতে পারে

অনেক সময় এটি SERIAL দিয়ে অটো-ইনক্রিমেন্ট করিয়ে রাখা হয়

উদাহরণ:
```sql
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    class INTEGER
);
```
এখানে student_id হচ্ছে Primary Key, যেটা প্রতিটি ছাত্রকে আলাদা করে চিহ্নিত করে।

Explain the Primary Key and Foreign Key concepts in PostgreSQL
PostgreSQL ব্যবহার করে যখন আমরা কোনো ডেটাবেজ তৈরি করি, তখন আমাদের অনেক সময় একাধিক টেবিল নিয়ে কাজ করতে হয়। আর এই টেবিলগুলোর মধ্যে সম্পর্ক তৈরি করতে এবং ডেটা ঠিকঠাক রাখতে দরকার হয় Primary Key আর Foreign Key এর ব্যবহার। নিচে আমি সহজভাবে ব্যাখ্যা করছি যেন যে কেউ বুঝতে পারে।

Primary Key কী?
Primary Key হলো টেবিলের এমন একটি ফিল্ড (বা একাধিক ফিল্ড একসাথে), যা প্রতিটি রেকর্ডকে আলাদা করে চিহ্নিত করতে সাহায্য করে। ধরুন আপনি একটি ছাত্রদের তথ্যের টেবিল তৈরি করলেন, তাহলে প্রতিটা ছাত্রকে আলাদা করে চেনার জন্য আপনাকে একটা ইউনিক আইডেন্টিফায়ার দিতে হবে। সেই কাজটাই করে Primary Key।

এই ফিল্ডে কোনো ডুপ্লিকেট ভ্যালু রাখা যায় না এবং এখানে NULL ও থাকা যাবে না। সাধারণত আমরা SERIAL টাইপ ব্যবহার করি যাতে প্রতিবার নতুন রেকর্ড যুক্ত হলে অটোমেটিক নতুন নাম্বার দেওয়া হয়।

উদাহরণ:

```sql
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    class INTEGER
);
```
এখানে student_id হলো Primary Key, যার মাধ্যমে প্রতিটা ছাত্র আলাদা হয়ে যাচ্ছে।

Foreign Key কী?
Foreign Key ব্যবহার করা হয় যখন আপনি এক টেবিলকে অন্য টেবিলের সাথে যুক্ত করতে চান। ধরুন, আপনার একটা courses নামে টেবিল আছে যেখানে কোর্সের তথ্য থাকে, আর আরেকটা enrollments নামে টেবিল আছে যেখানে ছাত্ররা কোন কোর্সে ভর্তি হয়েছে তার তথ্য রাখা হয়। এখন এই দুই টেবিলকে যুক্ত করতে enrollments টেবিলে course_id নামে একটি ফিল্ড রাখবেন, যেটা courses টেবিলের course_id ফিল্ডের সাথে সম্পর্কিত থাকবে। এই course_id-কে তখন Foreign Key বলা হয়।

Foreign Key নিশ্চিত করে যে আপনি এমন কোনো কোর্স আইডি দিতে পারবেন না যেটা courses টেবিলে নেই। এর ফলে ভুল ডেটা ঢুকার সম্ভাবনা কমে যায় এবং ডেটাবেজে সঠিকতা বজায় থাকে।

উদাহরণ:

```sql
CREATE TABLE courses (
    course_id SERIAL PRIMARY KEY,
    course_name VARCHAR(100)
);

CREATE TABLE enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_id INT,
    course_id INT,
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```
এখানে enrollments টেবিলের course_id ফিল্ডটি courses টেবিলের course_id কে রেফার করছে। তাই কেউ যখন কোন কোর্সে ভর্তি হবে, তখন সেটা অবশ্যই courses টেবিলে আগে থেকে থাকতে হবে।

কেন এগুলো দরকার?
Primary Key আমাদের প্রতিটি রেকর্ডকে আলাদা করে চিনতে সাহায্য করে। এতে করে ডেটা খুঁজে পাওয়া, আপডেট বা ডিলিট করাটা সহজ এবং নির্ভরযোগ্য হয়।

Foreign Key আমাদের একাধিক টেবিলের মধ্যে সংযোগ তৈরি করতে দেয়। এতে করে আমরা ডেটার মধ্যে সঠিক সম্পর্ক বজায় রাখতে পারি এবং ভুল ডেটা ঢুকতে বাধা দেওয়া যায়।


##3, What is the difference between the VARCHAR and CHAR data types?
## CHAR কী?

`CHAR` হলো এমন একটা টাইপ, যেটা সবসময় ঠিক যত জায়গা তুমি দাও, ততটুকু ব্যবহার করে।  
ধরো তুমি বললা `CHAR(5)` — এখন তুমি শুধু "BD" দাও, তাও সে পেছনে ৩টা ফাঁকা জায়গা দিয়ে রাখবে, যেন সবসময় ৫ অক্ষরের মতো লাগে।

**যেমন:**

```sql
CREATE TABLE test (
  country_code CHAR(5)
);

INSERT INTO test VALUES ('BD');
এইখানে আসলে ডেটা যেভাবে জমা হবে: 'BD ' (BD আর তিনটা ফাঁকা জায়গা)

ব্যবহার করো কবে:

যখন সব ডেটা সাইজে সমান হয়

যেমন: Country Code, Gender, বা Y/N টাইপ ফিল্ড

VARCHAR কী?
VARCHAR একটু স্মার্ট টাইপ। তুমি যত অক্ষর দিবা, ও ততটুকুই রাখবে। একটুও বাড়তি স্পেস রাখবে না।

যেমন:

```sql
CREATE TABLE test2 (
  name VARCHAR(20)
);
```

INSERT INTO test2 VALUES ('Rakib');
এখানে শুধু 'Rakib' থাকবে। শেষে কোনো স্পেস-টেস থাকবে না।


## 4, What is the purpose of a database schema in PostgreSQL?

## Schema আসলে কী?

Schema মানে হচ্ছে ডেটাবেজের ভেতরে একটা আলাদা ঘর বা ফোল্ডার — যেটার মধ্যে টেবিল, ভিউ, ফাংশন এসব রাখা যায়।

এক কথায় বললে: **একটা ডেটাবেজের ভিতরে আলাদা আলাদা গুচ্ছ করে জিনিসপত্র রাখার ব্যবস্থা।**

---

## উদাহরণ দেই

ধরো, একটা ডেটাবেজ আছে `company_db` নামে।

এখন তুমি চাও HR-এর টেবিল আর Accounts-এর টেবিল গুলা আলাদা রাখতে। তখন করবা দুইটা স্কিমা:

- `hr` স্কিমার মধ্যে থাকবে: `employees`, `departments` টেবিল
- `accounts` স্কিমার মধ্যে থাকবে: `salaries`, `expenses` টেবিল

এতে করে এক ডেটাবেজেই সব কিছু থাকবে, কিন্তু গুছানোভাবে।

---

## কেন Schema ব্যবহার করবো?

- **গোছানো থাকে:** আলাদা আলাদা টেবিল গুলা আলাদা গ্রুপে রাখা যায়
- **সিকিউরিটি কন্ট্রোল:** স্কিমা ধরে ধরে পারমিশন দেওয়া যায় (কে কোন স্কিমা একসেস করতে পারবে)
- **কনফ্লিক্ট কমায়:** দুই স্কিমাতে একই নামের টেবিল থাকতে পারে — সমস্যা হবে না

```sql
-- hr স্কিমাতে employees টেবিল
SELECT * FROM hr.employees;

-- accounts স্কিমাতে employees টেবিল থাকলেও সমস্যা নাই
SELECT * FROM accounts.employees;

```

## 5, Explain the purpose of the WHERE clause in a SELECT statement.

`WHERE` clause ব্যবহার করা হয় যখন আমরা SELECT, UPDATE, DELETE করার সময় ডেটা থেকে বিশেষ কিছু শর্ত অনুযায়ী ডেটা নিতে বা কাজ করতে চাই।

সোজা ভাষায়, `WHERE` দিয়ে বলে দিতে পারি, "সব ডেটা না নিয়ে, শুধু যেগুলো আমার শর্ত মেটায়, সেগুলোই নিয়ে আসো বা কাজ করো।"

### উদাহরণ:

```sql
SELECT * FROM students WHERE class = 10;
```
এখানে students টেবিল থেকে শুধু সেইসব ছাত্রের তথ্য দেখাবে যাদের ক্লাস ১০।

আরেকটা উদাহরণ:
```sql


SELECT * FROM employees WHERE salary > 30000;
```
এখানে সেলেক্ট করবে শুধুমাত্র যাদের বেতন ৩০০০০ এর বেশি।

মূল কাজ:
ডেটা ফিল্টার করা

নির্দিষ্ট শর্ত অনুযায়ী রেকর্ড বেছে নেওয়া

বড় বড় টেবিল থেকে দরকারি ডেটা দ্রুত পাওয়া