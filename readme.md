## What is PostgreSQL?

**উত্তর:**

PostgreSQL একটি শক্তিশালী, Open Source **রিলেশনাল ডেটাবেজ ম্যানেজমেন্ট সিস্টেম (RDBMS)**। এটি SQL (Structured Query Language) ব্যবহার করে ডেটা সংরক্ষণ, অনুসন্ধান, আপডেট এবং মুছে ফেলার কাজ করে।
PostgreSQL বিশ্বের অন্যতম জনপ্রিয় এবং উন্নত ডেটাবেজ সফটওয়্যার, যা ছোট অ্যাপ্লিকেশন থেকে শুরু করে বড় কোম্পানির Scalable সিস্টেমেও Use হয়।

---

## PostgreSQL এর বৈশিষ্ট্যসমূহ

- ✅ **অ্যাডভান্সড কুয়েরি সাপোর্ট** – জটিল SQL কুয়েরি সহজে করা যায়।
- ✅ **ACID কমপ্লায়েন্ট** – Atomicity, Consistency, Isolation, Durability মেনে চলে।
- ✅ **MVCC (Multi-Version Concurrency Control)** – একাধিক ইউজার একই ডেটার উপর কাজ করতে পারে।
- ✅ **JSON সাপোর্ট** – রিলেশনাল ও নন-রিলেশনাল ডেটা দুভাবেই সংরক্ষণযোগ্য।

---

## কেন PostgreSQL ব্যবহার করবেন?

1. **বিনামূল্যে ব্যবহারের সুবিধা** – কোনো লাইসেন্স ফি নেই।
2. **কমিউনিটি সাপোর্ট** – প্রচুর ডকুমেন্টেশন ও Uer ফোরাম রয়েছে।
3. **উচ্চ পারফরম্যান্স** – বড় ডেটা নিয়েও দ্রুত কাজ করে।
4. **ডেটা নিরাপত্তা ও নির্ভরযোগ্যতা** – Enterprise Grade ফিচার রয়েছে।

---

## উদাহরণ:

ধরুন আপনি একটি স্কুলের ছাত্রদের তথ্য সংরক্ষণ করতে চান। PostgreSQL দিয়ে নিচের মতো একটি টেবিল তৈরি করতে পারেন:

```sql
CREATE TABLE students (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  class INTEGER,
  admission_date DATE
);
```
এখানে students নামে একটি টেবিল তৈরি হয়েছে যেখানে প্রতিটি ছাত্রের নাম, ক্লাস এবং ভর্তি তারিখ সংরক্ষণ করা যাবে।



## What is the purpose of a database schema in PostgreSQL?

**উত্তর:**


PostgreSQL-এ ডেটাবেজ ডিজাইনের সময় টেবিলগুলোর মধ্যে relationship তৈরি এবং data integrity বজায় রাখতে **Primary Key** এবং **Foreign Key** গুরুত্বপূর্ণ ভূমিকা পালন করে।

---

## 🗝️ Primary Key কী?

**Primary Key** হল এমন একটি কলাম (বা কলামগুলোর সমষ্টি), যা প্রতিটি রেকর্ডকে **অন্য সব রেকর্ড থেকে আলাদা** করে। এই ফিল্ডে Duplicate ভ্যালু বা `NULL` থাকতে পারে না।

### ✅ বৈশিষ্ট্যসমূহ:

- প্রতিটি রেকর্ড Unique হয়
- `NULL` মান গ্রহণ করে না
- টেবিলে শুধুমাত্র একটি Primary Key থাকতে পারে
- অটো-ইনক্রিমেন্ট বা SERIAL ব্যবহার করা যায়

### 🧪 উদাহরণ:
```sql
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    class INTEGER
);
```
উপরের students টেবিলে student_id কলামটি হল Primary Key। এটি স্বয়ংক্রিয়ভাবে (SERIAL) বাড়ে এবং প্রতিটি ছাত্রের জন্য Qunique ID নির্ধারণ করে।

🔗 Foreign Key কী?
Foreign Key এমন একটি কলাম যা অন্য একটি টেবিলের Primary Key-এর সাথে সম্পর্ক তৈরি করে। এটি দুটি টেবিলের মধ্যে logical connection তৈরি করে এবং ডেটার মধ্যে referential integrity নিশ্চিত করে।

✅ বৈশিষ্ট্যসমূহ:
অন্য টেবিলের Primary Key কে রেফার করে

Data Link বা Relation তৈরি করে

অনেক সময় একাধিক Foreign Key থাকতে পারে

রেফারেন্স করা রেকর্ড না থাকলে ইনসার্ট করা যায় না

🧪 উদাহরণ:
sql
Copy
Edit
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
এখানে enrollments.course_id কলামটি courses.course_id এর প্রতি রেফার করে। অর্থাৎ, একটি কোর্সে রেজিস্ট্রেশন করতে হলে সেই কোর্সটি courses টেবিলে আগে থেকেই থাকতে হবে।

🎯 কেন গুরুত্বপূর্ণ?
Primary Key:
প্রতিটি রেকর্ডের জন্য ইউনিক আইডি নির্ধারণ করে

সার্চ, আপডেট, ডিলিট অপারেশনকে নির্ভরযোগ্য করে তোলে

Foreign Key:
টেবিলগুলোর মধ্যে সম্পর্ক তৈরি করে

ডেটার মধ্যে ভুল ঢুকানো রোধ করে

ডেটাবেজে consistency বজায় রাখে

