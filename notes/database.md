# 数据库系统概论 (Introduction to Database Systems) —— APS 核心复习笔记

> **APS 备考指导 (Exam Strategy)**：
> * **课程定位**：Fall 2024（3.5 学分）。对于**物联网工程 (IoT Engineering)** 专业，德国 APS 审核官在考察《数据库系统概论》时，**极少**让你推导复杂的“关系代数公式”或手算“闭包/BCNF分解”，而是重点考核以下 **4 件事**：
>   1. **建模能力**：能画简单的 **E-R 图**，并知道怎么把实体和联系（特别是 `1:N` 和 `M:N`）转换成**关系表 (Tables)**。
>   2. **SQL 实战**：考官常在纸上给出 2 张简单表，让你手写 3~5 行 **`SELECT` + `JOIN` + `GROUP BY`** 语句。
>   3. **核心概念**：能用英语说清楚 **Primary Key / Foreign Key**、**1NF/2NF/3NF（为什么需要范式）**、以及事务的 **ACID** 特性。
>   4. **专业结合**：知道物联网设备产生大量传感器数据时，传统关系型数据库（MySQL）与非关系型/时序数据库（NoSQL / Time-Series DB）的简单区别。
>
> 本笔记剔除深奥的底层存储算法与繁琐证明，保留**最核心的概念 + 极简实例 + 英语口述表达**。

---

## 目录 (Quick Navigation)
1. [数据库系统基础概念 (Database Fundamentals)](#1-数据库系统基础概念-database-fundamentals)
2. [概念模型：E-R 图与表转换 (E-R Modeling & Table Mapping)](#2-概念模型e-r-图与表转换-e-r-modeling--table-mapping)
3. [关系模型与完整性约束 (Relational Model & Integrity Constraints)](#3-关系模型与完整性约束-relational-model--integrity-constraints)
4. [SQL 核心语法与必考查询 (Core SQL Operations)](#4-sql-核心语法与必考查询-core-sql-operations)
5. [数据库规范化：1NF / 2NF / 3NF (Normalization)](#5-数据库规范化1nf--2nf--3nf-normalization)
6. [事务与并发控制基础 (Transactions & ACID)](#6-事务与并发控制基础-transactions--acid)
7. [索引与视图简介 (Indexes & Views)](#7-索引与视图简介-indexes--views)
8. [RDBMS vs. NoSQL 与物联网应用 (IoT Context)](#8-rdbms-vs-nosql-与物联网应用-iot-context)
9. [APS 考场高频问答速查表 (Oral Q&A Cheat Sheet)](#9-aps-考场高频问答速查表-oral-qa-cheat-sheet)

---

## 1. 数据库系统基础概念 (Database Fundamentals)

### 1.1 四个核心缩写
* **Data (数据)**：描述事物的符号记录（如传感器测得的温度值 `26.5`）。
* **DB (Database，数据库)**：长期存储在计算机内、有组织的、可共享的大量数据的集合。
* **DBMS (Database Management System，数据库管理系统)**：管理数据库的软件系统（如 MySQL, PostgreSQL, Oracle），负责数据的增删改查、安全性和并发控制。
* **DBS (Database System，数据库系统)**：包含 `DB + DBMS + 应用程序 + DBA (数据库管理员)` 的整体。

### 1.2 为什么用数据库，而不用普通文件 (File System vs. DBMS)？
早期用 TXT/CSV 文件存数据有三大痛点，DBMS 完美解决了它们：
1. **减少数据冗余 (Less Redundancy)**：同一份信息不用在多个文件里重复保存。
2. **保证数据一致性与并发安全 (Consistency & Concurrency)**：多人同时修改不会写乱。
3. **提供数据独立性 (Data Independence)**：改了底层存储方式或加了新字段，外面的应用程序不用跟着重写。

### 1.3 三级模式结构 (Three-Schema Architecture) —— 了解即可
为了实现“数据独立性”，数据库在逻辑上分三层：
* **外模式 (External Schema / View)**：用户或程序看到的局部数据视图（如只看到某几个字段）。
* **模式 (Conceptual Schema / Logical Schema)**：所有表和关系的全局逻辑结构（核心层）。
* **内模式 (Internal Schema / Physical Schema)**：数据在磁盘上到底怎么存的（文件、索引、存储路径）。

> **APS 一句话总结**：
> *"A DBMS is software like MySQL that stores, organizes, and secures data, solving problems of plain files such as redundancy, inconsistency, and concurrent access."*

---

## 2. 概念模型：E-R 图与表转换 (E-R Modeling & Table Mapping)

在写代码建表之前，先用 **E-R 图 (Entity-Relationship Diagram)** 进行概念设计。

### 2.1 E-R 图三要素
* **实体 (Entity)**：现实世界中独立存在的事物（用**矩形**表示），例如：`Device`（设备）、`Sensor`（传感器）、`User`（用户）。
* **属性 (Attribute)**：实体的特征（用**椭圆**表示），例如设备有 `device_id`、`location`、`status`。
* **联系 (Relationship)**：实体之间的关系（用**菱形**表示），主要分三种基数比：
  * **1:1 (One-to-One)**：一个用户对应一份个人详情资料。
  * **1:N (One-to-Many)**：一个网关 (Gateway) 下挂多个传感器节点 (Sensor)。
  * **M:N (Many-to-Many)**：一个学生可以选多门课，一门课也可以被多个学生选。

### 2.2 极简实例：物联网设备管理 E-R 转关系表（必考！）
假设我们有 `User` 和 `Device`、`Tag`：

1. **1:N 联系的转换（多的一方加外键）**：
   一个用户 (`User`) 拥有多个设备 (`Device`)。
   * `User(user_id [PK], username)`
   * `Device(device_id [PK], device_name, user_id [FK])` $\rightarrow$ **把“1”的主键放进“N”的表里作外键。**

2. **M:N 联系的转换（必须新建一张中间表）**：
   一个学生 (`Student`) 选多门课 (`Course`)，一门课有多个学生。
   * `Student(student_id [PK], name)`
   * `Course(course_id [PK], title)`
   * `Enrollment(student_id [PK, FK], course_id [PK, FK], score)` $\rightarrow$ **拆出第三张关联表，存放双方的主键。**

> **APS 一句话总结**：
> *"An E-R diagram models entities, attributes, and relationships. When converting to tables, a 1-to-N relationship puts the parent's primary key as a foreign key in the child table, while an M-to-N relationship requires a new junction table."*

---

## 3. 关系模型与完整性约束 (Relational Model & Integrity Constraints)

在关系型数据库中，数据以二维**表 (Table / Relation)** 的形式存储：
* **行 (Row / Tuple / 元组)**：一条具体的数据记录。
* **列 (Column / Attribute / 属性)**：一个数据字段。

### 3.1 键的概念 (Keys)
* **候选键 (Candidate Key)**：能**唯一标识**一行记录的最小属性集合（比如身份证号和学号都可以唯一确定一个学生，都是候选键）。
* **主键 (Primary Key, PK)**：从候选键中选出的**唯一代表**（如选 `student_id` 作主键）。**要求：非空 (NOT NULL) 且唯一 (UNIQUE)**。
* **外键 (Foreign Key, FK)**：表 A 中的某个字段，引用表 B 的主键。**作用：建立两张表之间的关联**。

### 3.2 三大完整性约束 (Integrity Constraints)
1. **实体完整性 (Entity Integrity)**：主键不能为空 (`NOT NULL`) 也不能重复 (`UNIQUE`)。否则无法区分两条记录。
2. **参照完整性 (Referential Integrity)**：外键的值，要么是关联表中真实存在的主键值，要么为 `NULL`（不能指向一个不存在的 ID）。
   * *例子*：如果 `User` 表里没有 `user_id = 99`，你就不能在 `Device` 表里插入一条 `user_id = 99` 的设备记录。
3. **用户自定义完整性 (User-Defined Integrity)**：业务层面的约束，如年龄 `age > 0`、温度在合理范围、邮箱不能为空。

> **APS 一句话总结**：
> *"A Primary Key uniquely identifies each row and cannot be null. A Foreign Key links to another table's Primary Key to ensure referential integrity."*

---

## 4. SQL 核心语法与必考查询 (Core SQL Operations)

SQL (Structured Query Language) 分为三类常用操作（加上权限控制 DCL，日常重点记住前三种即可）：

### 4.1 DDL (Data Definition Language，定义结构)
用于创建、修改、删除表结构：
```sql
CREATE TABLE Device (
    device_id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    room_id INT,
    FOREIGN KEY (room_id) REFERENCES Room(room_id)
);
```
* 常用关键词：`CREATE`, `ALTER` (修改表结构), `DROP` (删表)。

### 4.2 DML (Data Manipulation Language，增删改数据)
```sql
-- 插入 (Insert)
INSERT INTO Device (device_id, name, room_id) VALUES (1, 'TempSensor_01', 101);

-- 更新 (Update) —— 面试一定要记得写 WHERE！
UPDATE Device SET name = 'TempSensor_A' WHERE device_id = 1;

-- 删除 (Delete)
DELETE FROM Device WHERE device_id = 1;
```

### 4.3 DQL (Data Query Language，查询数据 —— 绝对重点！)
**经典查询结构**：
```sql
SELECT room_id, COUNT(*) AS sensor_count
FROM Device
WHERE status = 'active'
GROUP BY room_id
HAVING COUNT(*) > 2
ORDER BY sensor_count DESC;
```
* **APS 高频对比：`WHERE` vs `HAVING`**：
  * `WHERE` 在**分组之前**过滤每一行原始数据（不能接 `COUNT()`、`AVG()` 等聚合函数）。
  * `HAVING` 在 `GROUP BY` **分组之后**过滤分组结果（可以接聚合函数）。

### 4.4 多表连接 (JOIN) —— 纸上写 SQL 高频考点
假设有 `Device(device_id, name, room_id)` 和 `Room(room_id, room_name)`：
```sql
-- INNER JOIN：只返回两张表都能匹配上的记录
SELECT Device.name, Room.room_name
FROM Device
INNER JOIN Room ON Device.room_id = Room.room_id;

-- LEFT JOIN：保留左表 (Device) 的所有记录，即使它还没分配房间 (room_name 显示为 NULL)
SELECT Device.name, Room.room_name
FROM Device
LEFT JOIN Room ON Device.room_id = Room.room_id;
```

> **APS 一句话总结**：
> *"SQL includes DDL like `CREATE TABLE`, DML like `INSERT`/`UPDATE`/`DELETE`, and DQL for querying. `WHERE` filters rows before grouping, while `HAVING` filters groups after `GROUP BY`. `INNER JOIN` returns matched rows, whereas `LEFT JOIN` keeps all rows from the left table."*

---

## 5. 数据库规范化：1NF / 2NF / 3NF (Normalization)

### 5.1 为什么要做规范化 (Why Normalize)?
如果把所有信息都塞进一张大表（比如把“设备信息 + 房间名称 + 管理员电话”全放进传感器读数表），会出现三大问题：
1. **数据冗余 (Data Redundancy)**：每上报一次温度，都要重复存一遍房间名称和管理员电话。
2. **更新异常 (Update Anomaly)**：管理员换电话了，得去改成千上万行记录，漏改一行数据就不一致了。
3. **插入/删除异常 (Insert/Delete Anomaly)**：刚建好一个新房间还没装传感器，房间信息就存不进去；删掉最后一个传感器，连带着这个房间的信息也丢了。

**解决办法**：按范式把大表拆分成结构合理的小表。

### 5.2 三大范式极简理解 (到 3NF 即可)

* **第一范式 (1NF - 原子性 Atomicity)**：
  * **要求**：表里的每一个格子（列）都**不可再分**。
  * *反例*：`sensors = "Temp_1, Hum_2"`（一格里塞了两个值）$\rightarrow$ 拆成多行或多列。

* **第二范式 (2NF - 消除部分依赖 No Partial Dependency)**：
  * **前提**：满足 1NF。
  * **要求**：当主键是**联合主键** `(A, B)` 时，其他非主属性必须依赖于**整个主键**，不能只依赖其中一部分（如只依赖 `A`）。
  * *例子*：表 `(student_id, course_id, score, student_name)`。联合主键是 `(student_id, course_id)`，但 `student_name` 只由 `student_id` 决定，与课程无关 $\rightarrow$ 把 `student_name` 拆回 `Student` 表。

* **第三范式 (3NF - 消除传递依赖 No Transitive Dependency)**：
  * **前提**：满足 2NF。
  * **要求**：非主属性之间不能互相决定（即不允许 `主键 -> A -> B` 这种传递链）。
  * *例子*：表 `(device_id [PK], room_id, room_location)`。`device_id` 决定 `room_id`，而 `room_id` 又决定了 `room_location` $\rightarrow$ 把 `room_location` 拆到独立的 `Room(room_id, room_location)` 表中。

> *(注：还有更严格的 BCNF，一般只需知道“日常设计做到 3NF 就足够解决绝大多数冗余问题”，有时候为了查询快甚至会刻意反范式化 Denormalization。)*

> **APS 一句话总结**：
> *"Normalization reduces redundancy and update anomalies. 1NF ensures atomic columns, 2NF removes partial dependencies on a composite key, and 3NF removes transitive dependencies between non-key attributes."*

---

## 6. 事务与并发控制基础 (Transactions & ACID)

### 6.1 什么是事务 (Transaction)?
事务是数据库操作的**最小逻辑工作单元**，里面的多条 SQL **要么全部成功，要么全部失败回滚 (Rollback)**。
* *经典例子*：A 给 B 转账 100 元（Step 1: A 扣 100；Step 2: B 加 100）。如果 Step 1 后断电了，必须回滚撤销 Step 1。

### 6.2 ACID 四大特性（必背！）
1. **A - Atomicity (原子性)**：要么全做，要么全不做（All or nothing），通过 Undo Log 实现回滚。
2. **C - Consistency (一致性)**：事务执行前后，数据库都处于合法状态（如转账前后两人总额不变）。
3. **I - Isolation (隔离性)**：多个并发事务之间互不干扰。
4. **D - Durability (持久性)**：一旦事务提交 (`COMMIT`)，修改就永久保存在磁盘中，即使系统崩溃也不会丢失。

### 6.3 并发问题与锁机制 (Concurrency & Locking) —— 简明概念
如果多个用户同时读写同一条数据，可能产生并发问题：
* **脏读 (Dirty Read)**：事务 A 读到了事务 B **尚未提交**的数据，结果 B 后来回滚了。
* **丢失更新 (Lost Update)**：两个事务同时改同一行，后提交的把先提交的覆盖了。

**如何解决？**
* **锁机制 (Locking)**：
  * **共享锁 / 读锁 (Shared Lock, S-Lock)**：大家可以同时读，但此时不能写。
  * **排他锁 / 写锁 (Exclusive Lock, X-Lock)**：我修改的时候，别人既不能读也不能写。
* **死锁 (Deadlock)**：两个事务互相等待对方手里的锁（类比《操作系统》里的死锁：打破循环等待或设置超时回滚即可解决）。

> **APS 一句话总结**：
> *"A transaction is an all-or-nothing unit of work guaranteed by ACID: Atomicity, Consistency, Isolation, and Durability. Locks (shared and exclusive) prevent concurrency anomalies like dirty reads."*

---

## 7. 索引与视图简介 (Indexes & Views)

### 7.1 索引 (Index)
* **是什么**：类似书本前面的**目录**。如果不加索引，查询一条记录需要逐行全表扫描 (Full Table Scan, $O(N)$)；加上索引（底层常用 **B+ 树** 结构）可以快速定位（$O(\log N)$）。
* **代价 (Trade-off)**：
  * **优点**：极大加快 `SELECT` 查询速度。
  * **缺点**：占用额外磁盘空间；每次 `INSERT / UPDATE / DELETE` 时，数据库都要顺便更新索引，**会降低写入速度**。所以不能给所有列都建索引。

### 7.2 视图 (View)
* **是什么**：基于 SQL 查询结果生成的**虚拟表 (Virtual Table)**，本身不单独存储数据。
* **作用**：
  1. **简化复杂查询**：把长串 `JOIN` 封装成一个视图，直接 `SELECT * FROM view_name`。
  2. **安全性 (Security)**：比如只给实习生开放包含 `name` 和 `department` 的视图，隐藏表里的 `salary` 字段。

---

## 8. RDBMS vs. NoSQL 与物联网应用 (IoT Context)

作为物联网工程学生，可以在回答末尾顺带展示专业视角：

| 对比维度 | 关系型数据库 (RDBMS, e.g. MySQL, PostgreSQL) | 非关系型 / 时序数据库 (NoSQL / TSDB, e.g. MongoDB, Redis, InfluxDB) |
| :--- | :--- | :--- |
| **数据结构** | 固定表结构 (Fixed Schema)，行和列 | 灵活结构 (JSON 文档、键值对、时间序列) |
| **事务支持** | 强一致性，完整支持 **ACID** | 侧重高可用与高吞吐，通常弱化 ACID (最终一致性) |
| **适用场景** | 用户账号、设备台账、权限、订单等结构化关系数据 | 海量高频传感器时序数据（温度/湿度流）、日志、缓存 |

* **IoT 典型架构一句话**：在实际物联网平台中，通常**混合使用**：用 **MySQL** 存储设备 ID、所属用户、告警规则等关系数据；用 **InfluxDB (时序库)** 或 **Redis** 接收并缓存高频上报的传感器采样流。

---

## 9. APS 考场高频问答速查表 (Oral Q&A Cheat Sheet)

| 高频问题 (Examiner's Question) | 考场核心回答思路 (Key Answer in English) |
| :--- | :--- |
| **1. What is a Primary Key vs. Foreign Key?** | *"A Primary Key uniquely identifies each row in a table and cannot be null. A Foreign Key is a column in one table that references the Primary Key of another table to link them together."* |
| **2. Explain 1NF, 2NF, and 3NF simply.** | *"Normalization reduces data redundancy. 1NF means every column holds atomic values. 2NF means every non-key attribute depends on the whole primary key. 3NF means non-key attributes do not depend on each other (no transitive dependency)."* |
| **3. What is the difference between `WHERE` and `HAVING`?** | *"Both filter data, but `WHERE` filters individual rows before grouping, whereas `HAVING` filters groups created by `GROUP BY` and can use aggregate functions like `COUNT()` or `AVG()`."* |
| **4. What is the difference between `INNER JOIN` and `LEFT JOIN`?** | *"`INNER JOIN` only returns rows that have matching values in both tables. `LEFT JOIN` returns all rows from the left table, and matching rows from the right table (or NULL if there is no match)."* |
| **5. What is ACID in transactions?** | *"Atomicity means all or nothing. Consistency ensures the database stays in a valid state. Isolation keeps concurrent transactions from interfering. Durability means committed changes are permanently saved."* |
| **6. Why not put an index on every column?** | *"Indexes speed up `SELECT` queries using structures like B+ Trees, but they take extra storage and slow down `INSERT`, `UPDATE`, and `DELETE` operations because the index must also be updated."* |
| **7. How do you model a Many-to-Many relationship?** | *"We cannot directly link two tables in M:N. Instead, we create a third junction table that contains the Primary Keys of both tables as Foreign Keys."* |
| **8. How would you store IoT sensor data?** | *"I would store structured metadata like device IDs and user info in a relational database like MySQL, and store high-frequency time-series sensor readings in a NoSQL or Time-Series database like InfluxDB for better write performance."* |
