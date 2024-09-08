# Oracle-SQL-DMLの使い方ガイド

このガイドでは、Oracle-SQL-DML（データ操作言語）を初めて使用する方々のために、基本的な操作方法と実際の使用例をステップバイステップで説明します。

## 1. データの挿入 (INSERT)
データベースに新しい行を追加するためには、`INSERT INTO`ステートメントを使用します。

### 例
```sql
INSERT INTO employees (employee_id, first_name, last_name, email)
VALUES (101, 'John', 'Doe', 'john.doe@example.com');
```
ここでは、`employees`テーブルに新しい従業員の情報を挿入しています。

## 2. データの更新 (UPDATE)
既存のデータを更新するには、`UPDATE`ステートメントを使用します。

### 例
```sql
UPDATE employees
SET email = 'john.newemail@example.com'
WHERE employee_id = 101;
```
この例では、`employee_id`が101の従業員のメールアドレスを更新しています。

## 3. データの削除 (DELETE)
特定の行を削除するには、`DELETE`ステートメントを使用します。

### 例
```sql
DELETE FROM employees
WHERE employee_id = 101;
```
このステートメントは、`employee_id`が101の従業員のデータを削除します。

## 4. データの選択 (SELECT)
データを選択して表示するには、`SELECT`ステートメントを使用します。

### 例
```sql
SELECT employee_id, first_name, last_name, email
FROM employees
WHERE department_id = 10;
```
このクエリは、`department_id`が10の全ての従業員の情報を表示します。

## 5. トランザクションの管理 (COMMIT と ROLLBACK)
データベースの変更を確定するには`COMMIT`、元に戻すには`ROLLBACK`を使用します。

### 例
```sql
-- データの挿入
INSERT INTO employees (employee_id, first_name, last_name, email)
VALUES (102, 'Jane', 'Smith', 'jane.smith@example.com');

-- 変更を確定
COMMIT;

-- データの更新
UPDATE employees
SET email = 'jane.newemail@example.com'
WHERE employee_id = 102;

-- 変更を元に戻す
ROLLBACK;
```
この例では、最初にデータを挿入してコミットし、その後の更新をロールバックしています。

## まとめ
このガイドでは、Oracle-SQL-DMLの基本的な操作方法を説明しました。これらのステートメントを使いこなすことで、データベースのデータを効率的に操作することができます。初めて使う場合でも、少しずつ練習していけばすぐに慣れるでしょう。