# Oracle-SQL-DDLの使い方ガイド

Oracle-SQL-DDL（データ定義言語）は、Oracleデータベースにおいてデータベースオブジェクトの定義や管理を行うためのSQLコマンド群です。このガイドでは、初心者向けにOracle-SQL-DDLの基本的な使い方をステップバイステップで説明します。

## 1. テーブルの作成

### コマンド: `CREATE TABLE`

新しいテーブルを作成するためのコマンドです。以下の例では、`employees`というテーブルを作成します。

```sql
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    hire_date DATE,
    salary NUMBER
);
```

### 説明:
- `employee_id`: 数値型で、主キー（PRIMARY KEY）として設定されます。
- `first_name`, `last_name`: 文字列型（VARCHAR2）で、最大50文字まで格納できます。
- `hire_date`: 日付型（DATE）。
- `salary`: 数値型（NUMBER）。

## 2. テーブルの変更

### コマンド: `ALTER TABLE`

既存のテーブルを変更するためのコマンドです。以下の例では、`employees`テーブルに新しいカラム`department_id`を追加します。

```sql
ALTER TABLE employees
ADD department_id NUMBER;
```

### 説明:
- `ADD department_id NUMBER;`: 新しいカラム`department_id`を数値型（NUMBER）で追加します。

## 3. テーブルの削除

### コマンド: `DROP TABLE`

不要になったテーブルを削除するためのコマンドです。以下の例では、`employees`テーブルを削除します。

```sql
DROP TABLE employees;
```

### 説明:
- `employees`テーブル全体が削除され、すべてのデータも失われます。

## 4. インデックスの作成

### コマンド: `CREATE INDEX`

特定のカラムにインデックスを作成して検索速度を向上させるためのコマンドです。以下の例では、`last_name`カラムにインデックスを作成します。

```sql
CREATE INDEX idx_last_name ON employees(last_name);
```

### 説明:
- `idx_last_name`: インデックスの名前。
- `employees(last_name)`: `employees`テーブルの`last_name`カラムにインデックスを作成。

## 5. ビューの作成

### コマンド: `CREATE VIEW`

複雑なクエリ結果を簡単に利用できるようにするための仮想テーブル（ビュー）を作成するコマンドです。以下の例では、`employee_salaries`というビューを作成します。

```sql
CREATE VIEW employee_salaries AS
SELECT employee_id, first_name, last_name, salary
FROM employees
WHERE salary > 50000;
```

### 説明:
- ビュー`employee_salaries`には、`employees`テーブルから給与が50,000を超える従業員のデータが含まれます。

## まとめ

Oracle-SQL-DDLはデータベースの構造を定義および管理するための強力なツールです。このガイドを参考に、基本的なDDLコマンドを理解し、実際に使用してみてください。練習を通じて、Oracleデータベースの管理スキルを向上させましょう。