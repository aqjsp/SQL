# MySQL查询语句全解

### 一、条件查询

#### 1. 基本 `SELECT` 语句

```
SELECT column1, column2 FROM table_name;
```

从 `table_name` 表中选择 `column1` 和 `column2` 列。

#### 2. 使用 `WHERE` 子句进行条件查询

`WHERE` 子句用于指定选择条件，只返回满足条件的记录。

示例

```
SELECT * FROM employees WHERE age > 30;
```

从 `employees` 表中选择所有年龄大于 30 的记录。

#### 3. 常用的条件运算符

- `=` : 等于
- `<>` 或 `!=` : 不等于
- `>` : 大于
- `<` : 小于
- `>=` : 大于或等于
- `<=` : 小于或等于

示例

```
SELECT * FROM products WHERE price <= 100;
```

从 `products` 表中选择价格小于或等于 100 的记录。

#### 4. 使用 `AND` 和 `OR` 组合条件

- `AND`：所有条件必须满足
- `OR`：任一条件满足即可

示例

```
SELECT * FROM employees WHERE age > 30 AND department = 'HR';
```

从 `employees` 表中选择年龄大于 30 且部门为 'HR' 的记录。

```
SELECT * FROM employees WHERE age > 30 OR department = 'HR';
```

从 `employees` 表中选择年龄大于 30 或部门为 'HR' 的记录。

#### 5. 使用 `IN` 和 `BETWEEN`

- `IN`：匹配列表中的任一值
- `BETWEEN`：在某个范围内

示例

```
SELECT * FROM employees WHERE department IN ('HR', 'IT', 'Finance');
```

从 `employees` 表中选择部门为 'HR', 'IT' 或 'Finance' 的记录。

```
SELECT * FROM products WHERE price BETWEEN 50 AND 100;
```

从 `products` 表中选择价格在 50 到 100 之间的记录。

#### 6. 使用 `LIKE` 进行模糊查询

`LIKE` 用于在 `WHERE` 子句中进行模糊查询，常与 `%` 和 `_` 通配符一起使用。

- `%`：表示零个或多个字符
- `_`：表示一个字符

示例

```
SELECT * FROM employees WHERE name LIKE 'J%';
```

从 `employees` 表中选择名称以 'J' 开头的记录。

```
SELECT * FROM employees WHERE name LIKE 'J_n';
```

从 `employees` 表中选择名称为三个字符且以 'J' 开头，中间任意一个字符，结尾为 'n' 的记录。

#### 7. 使用 `IS NULL` 和 `IS NOT NULL`

- `IS NULL`：检查某列是否为 `NULL`
- `IS NOT NULL`：检查某列是否不为 `NULL`

示例

```
SELECT * FROM employees WHERE manager_id IS NULL;
```

从 `employees` 表中选择 `manager_id` 为 `NULL` 的记录。

```
SELECT * FROM employees WHERE manager_id IS NOT NULL;
```

从 `employees` 表中选择 `manager_id` 不为 `NULL` 的记录。

#### 综合示例

```
SELECT name, department, salary
FROM employees
WHERE age > 30 AND department IN ('HR', 'IT');
```

从 `employees` 表中选择年龄大于 30 且部门为 'HR' 或 'IT' 的员工姓名、部门和工资。

### 二、排序

#### 1. 基本排序语句

`ORDER BY` 子句用于按指定的列对查询结果进行排序。默认情况下，排序是升序的。

示例

```
SELECT * FROM employees ORDER BY salary;
```

从 `employees` 表中选择所有记录，并按 `salary` 升序排序。

#### 2. 指定排序顺序

可以使用 `ASC` 指定升序，或使用 `DESC` 指定降序。

示例

```
SELECT * FROM employees ORDER BY salary DESC;
```

从 `employees` 表中选择所有记录，并按 `salary` 降序排序。

#### 3. 按多列排序

可以按多列排序，先按第一列排序，再按第二列排序，以此类推。

示例

```
SELECT * FROM employees ORDER BY department, salary DESC;
```

从 `employees` 表中选择所有记录，先按 `department` 升序排序，再按 `salary` 降序排序。

#### 4. 使用别名排序

可以使用列的别名进行排序。

示例

```
SELECT name, salary AS employee_salary FROM employees ORDER BY employee_salary;
```

从 `employees` 表中选择 `name` 和 `salary` 列，并按 `employee_salary` 别名升序排序。

#### 5. 混合使用升序和降序

可以在同一个查询中混合使用升序和降序。

示例

```
SELECT * FROM employees ORDER BY department ASC, salary DESC;
```

从 `employees` 表中选择所有记录，先按 `department` 升序排序，再按 `salary` 降序排序。

#### 6. 对计算列排序

可以对计算列进行排序。

示例

```
SELECT name, salary, salary * 1.1 AS new_salary FROM employees ORDER BY new_salary;
```

从 `employees` 表中选择 `name`、`salary` 和计算列 `new_salary`，并按 `new_salary` 升序排序。

#### 7. `ORDER BY` 与 `LIMIT` 结合使用

可以将 `ORDER BY` 与 `LIMIT` 子句结合使用，获取排序后的前几条记录。

示例

```
SELECT * FROM employees ORDER BY salary DESC LIMIT 5;
```

从 `employees` 表中选择所有记录，并按 `salary` 降序排序，仅返回前五条记录。

#### 8. `ORDER BY` 与 `GROUP BY` 结合使用

可以将 `ORDER BY` 与 `GROUP BY` 子句结合使用，先分组再排序。

示例

```
SELECT department, AVG(salary) AS avg_salary FROM employees GROUP BY department ORDER BY avg_salary DESC;
```

从 `employees` 表中选择 `department` 和平均 `salary`，按 `department` 分组，并按平均 `salary` 降序排序。

#### 综合示例

```
SELECT department, name, salary
FROM employees
WHERE age > 30
ORDER BY department ASC, salary DESC;
```

从 `employees` 表中选择 `department`、`name` 和 `salary`，仅返回年龄大于 30 的员工记录，先按 `department` 升序排序，再按 `salary` 降序排序。

### 三、聚合函数

#### 1. `COUNT()`

计算表中记录的数量，通常用于计数满足条件的行数。

示例

```
SELECT COUNT(*) FROM employees;
```

计算 `employees` 表中的总行数。

#### 2. `SUM()`

计算指定列的总和，通常用于数值列。

示例

```
SELECT SUM(salary) FROM employees;
```

计算 `employees` 表中 `salary` 列的总和。

#### 3. `AVG()`

计算指定列的平均值，通常用于数值列。

示例

```
SELECT AVG(salary) FROM employees;
```

计算 `employees` 表中 `salary` 列的平均值。

#### 4. `MAX()`

返回指定列的最大值。

示例

```
SELECT MAX(salary) FROM employees;
```

返回 `employees` 表中 `salary` 列的最大值。

#### 5. `MIN()`

返回指定列的最小值。

示例

```
SELECT MIN(salary) FROM employees;
```

返回 `employees` 表中 `salary` 列的最小值。

#### 6. `GROUP BY` 与聚合函数结合

`GROUP BY` 子句用于将结果集按一个或多个列进行分组，然后对每个分组应用聚合函数。

示例

```
SELECT department, AVG(salary) 
FROM employees 
GROUP BY department;
```

按 `department` 分组，并计算每个部门的平均 `salary`。

#### 7. `HAVING` 子句

`HAVING` 子句用于过滤分组后的结果，常与 `GROUP BY` 子句结合使用。

示例

```
SELECT department, AVG(salary) 
FROM employees 
GROUP BY department 
HAVING AVG(salary) > 50000;
```

按 `department` 分组，并筛选出平均 `salary` 大于 50000 的部门。

#### 综合示例

```
SELECT department, COUNT(*), AVG(salary), MAX(salary), MIN(salary) 
FROM employees 
GROUP BY department;
```

按 `department` 分组，并返回每个部门的员工数、平均 `salary`、最高 `salary` 和最低 `salary`。

### 四、分组

在 MySQL 中，分组操作可以通过 `GROUP BY` 子句来实现，它用于将结果集按一个或多个列进行分组。分组后，您可以对每个分组应用聚合函数，如 `COUNT()`、`SUM()`、`AVG()`、`MAX()` 和 `MIN()` 等。下面是详细的解释和示例。

#### 基本语法

```
SELECT column1, column2, ..., aggregate_function(column)
FROM table_name
GROUP BY column1, column2, ...;
```

示例

假设有一个名为 `employees` 的表，结构如下：

```
CREATE TABLE employees (
    id INT,
    name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10, 2)
);
```

#### 1. 按部门分组并计算每个部门的员工数量

```
SELECT department, COUNT(*) AS num_employees
FROM employees
GROUP BY department;
```

输出示例：

```
+------------+---------------+
| department | num_employees |
+------------+---------------+
| HR         | 10            |
| Sales      | 15            |
| IT         | 20            |
+------------+---------------+
```

#### 2. 按部门分组并计算每个部门的平均工资

```
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

输出示例：

```
+------------+------------+
| department | avg_salary |
+------------+------------+
| HR         | 50000.00   |
| Sales      | 60000.00   |
| IT         | 70000.00   |
+------------+------------+
```

#### 3. 使用 `HAVING` 过滤分组结果

`HAVING` 子句用于过滤分组后的结果，与 `WHERE` 子句不同的是，`HAVING` 作用于聚合后的结果。

```
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 55000;
```

输出示例：

```
+------------+------------+
| department | avg_salary |
+------------+------------+
| Sales      | 60000.00   |
| IT         | 70000.00   |
+------------+------------+
```

#### 4. 多列分组

您可以根据多个列进行分组。

```
SELECT department, name, SUM(salary) AS total_salary
FROM employees
GROUP BY department, name;
```

输出示例：

```
+------------+---------+--------------+
| department | name    | total_salary |
+------------+---------+--------------+
| HR         | Alice   | 30000.00     |
| HR         | Bob     | 20000.00     |
| Sales      | Carol   | 40000.00     |
| Sales      | Dave    | 20000.00     |
| IT         | Eve     | 50000.00     |
| IT         | Frank   | 20000.00     |
+------------+---------+--------------+
```

#### 注意事项

1. `GROUP BY` 子句中的列应当出现在 `SELECT` 语句中，除非使用聚合函数。
2. `HAVING` 子句用于过滤聚合后的结果，而 `WHERE` 子句用于过滤聚合前的数据。
3. `GROUP BY` 子句会影响查询的性能，尤其是大数据集上，优化索引和查询非常重要。

### 五、连接查询

#### 1. 内连接 (INNER JOIN)

内连接返回两个表中满足连接条件的交集记录。

```
SELECT a.column1, b.column2
FROM table1 a
INNER JOIN table2 b
ON a.common_column = b.common_column;
```

示例：

```
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.id;
```

#### 2. 左连接 (LEFT JOIN) 或左外连接 (LEFT OUTER JOIN)

左连接返回左表的所有记录及右表中满足连接条件的记录，没有匹配的记录则结果中包含NULL。

```
SELECT a.column1, b.column2
FROM table1 a
LEFT JOIN table2 b
ON a.common_column = b.common_column;
```

示例：

```
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.id;
```

#### 3. 右连接 (RIGHT JOIN) 或右外连接 (RIGHT OUTER JOIN)

右连接返回右表的所有记录及左表中满足连接条件的记录，没有匹配的记录则结果中包含NULL。

```
SELECT a.column1, b.column2
FROM table1 a
RIGHT JOIN table2 b
ON a.common_column = b.common_column;
```

示例：

```
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.id;
```

#### 4. 全连接 (FULL JOIN) 或全外连接 (FULL OUTER JOIN)

全连接返回左右表中所有记录，无论是否满足连接条件，不支持在MySQL中，可以通过左连接和右连接的联合实现。

```
SELECT a.column1, b.column2
FROM table1 a
LEFT JOIN table2 b
ON a.common_column = b.common_column
UNION
SELECT a.column1, b.column2
FROM table1 a
RIGHT JOIN table2 b
ON a.common_column = b.common_column;
```

示例：

```
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.id
UNION
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.id;
```

#### 5. 自连接 (Self Join)

自连接是指一个表与自身的连接，常用于树状数据结构的查询。

```
SELECT a.column1, b.column2
FROM table1 a
INNER JOIN table1 b
ON a.common_column = b.common_column;
```

示例：

```
SELECT e1.name AS employee, e2.name AS manager
FROM employees e1
INNER JOIN employees e2
ON e1.manager_id = e2.id;
```

#### 6. 交叉连接 (CROSS JOIN)

交叉连接返回两个表的笛卡尔积，即所有可能的记录组合。

```
SELECT a.column1, b.column2
FROM table1 a
CROSS JOIN table2 b;
```

示例：

```
SELECT employees.name, departments.department_name
FROM employees
CROSS JOIN departments;
```

### 六、子查询

MySQL 子查询是指在另一个 SQL 语句中嵌套的查询，通常用于复杂查询场景。子查询可以出现在 SELECT、INSERT、UPDATE、DELETE 语句中的 WHERE、HAVING、FROM 子句等位置。

#### 1. 在 SELECT 语句中的子查询

```
SELECT column1
FROM table1
WHERE column2 = (SELECT column2 FROM table2 WHERE condition);
```

示例：

```
SELECT name
FROM employees
WHERE department_id = (SELECT id FROM departments WHERE name = 'Sales');
```

此查询返回所有属于“Sales”部门的员工名字。

#### 2. 在 FROM 子句中的子查询

子查询作为临时表使用：

```
SELECT a.column1, b.column2
FROM (SELECT column1, column2 FROM table1) a
JOIN table2 b ON a.column1 = b.column1;
```

示例：

```
SELECT dept_employee.name, department.total_sales
FROM (SELECT id, name FROM employees) AS dept_employee
JOIN (SELECT department_id, SUM(sales) AS total_sales FROM sales GROUP BY department_id) AS department
ON dept_employee.id = department.department_id;
```

#### 3. 在 HAVING 子句中的子查询

```
SELECT column1, SUM(column2)
FROM table1
GROUP BY column1
HAVING SUM(column2) > (SELECT AVG(column2) FROM table1);
```

示例：

```
SELECT department_id, SUM(salary)
FROM employees
GROUP BY department_id
HAVING SUM(salary) > (SELECT AVG(salary) FROM employees);
```

此查询返回总薪资高于平均薪资的部门 ID 和其总薪资。

#### 4. 在 UPDATE 语句中的子查询

```
UPDATE table1
SET column1 = (SELECT expression FROM table2 WHERE condition)
WHERE condition;
```

示例：

```
UPDATE employees
SET salary = (SELECT AVG(salary) FROM employees)
WHERE department_id = 1;
```

此查询将部门 ID 为 1 的员工薪资设置为公司平均薪资。

#### 5. 在 DELETE 语句中的子查询

```
DELETE FROM table1
WHERE column1 = (SELECT column1 FROM table2 WHERE condition);
```

示例：

```
DELETE FROM employees
WHERE department_id = (SELECT id FROM departments WHERE name = 'HR');
```

此查询删除属于“HR”部门的所有员工记录。

#### 6. 相关子查询

相关子查询依赖于外部查询中的数据：

```
SELECT column1
FROM table1
WHERE EXISTS (SELECT 1 FROM table2 WHERE table1.column2 = table2.column2);
```

示例：

```
SELECT e.name
FROM employees e
WHERE EXISTS (SELECT 1 FROM departments d WHERE e.department_id = d.id AND d.name = 'HR');
```

此查询返回所有属于“HR”部门的员工名字。