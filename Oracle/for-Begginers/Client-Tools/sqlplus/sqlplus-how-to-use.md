# How to Use SQL*Plus

SQL*Plusの基本的な使用方法を、具体的な例を交えて説明します。

## 1. SQL*Plusの起動

コマンドプロンプトまたはターミナルから以下のように入力します：

```
sqlplus username/password@database
```

例：
```
sqlplus scott/tiger@orcl
```


また、sys as sysdbaをつけることで特権ユーザで接続することができます。
これはLinuxのOracleユーザとともにOS認証の接続で利用されます。

```
su - oracle
```

```
sqlplus / as sysdba@database
```

## 2. 基本的なSQLコマンドの実行

接続後、SQLコマンドを直接入力できます。

例：テーブル一覧の表示
```sql
SQL> SELECT table_name FROM user_tables;
```

例：データの挿入
```sql
SQL> INSERT INTO employees (employee_id, first_name, last_name) 
     VALUES (1001, 'John', 'Doe');
```

## 3. SQL*Plusコマンドの使用

SQL*Plus特有のコマンドも利用できます。これらは通常、スラッシュ（/）で始まります。

例：現在の日付の表示
```sql
SQL> SELECT SYSDATE FROM DUAL;
```

例：コマンドの履歴表示
```
SQL> HISTORY
```

## 4. 出力フォーマットの設定

結果の表示形式をカスタマイズできます。

例：列幅の設定
```
SQL> COLUMN first_name FORMAT A15
SQL> SELECT first_name, last_name FROM employees;
```

## 5. スクリプトの実行

SQLコマンドを記述したファイルを実行できます。

例：`query.sql`というファイルを実行
```
SQL> @query.sql
```

## 6. セッションの終了

SQL*Plusを終了するには以下のコマンドを使用します：

```
SQL> EXIT
```

または

```
SQL> QUIT
```

## 便利なTips

- `DESCRIBE`コマンドでテーブル構造を確認できます：
  ```
  SQL> DESCRIBE employees
  ```

- `SHOW`コマンドで現在の設定を確認できます：
  ```
  SQL> SHOW LINESIZE
  ```

- `SPOOL`コマンドで出力を文件に保存できます：
  ```
  SQL> SPOOL output.txt
  SQL> SELECT * FROM employees;
  SQL> SPOOL OFF
  ```

これらの基本的な操作を習得することで、SQL*Plusを効果的に使用し始めることができます。練習を重ねるにつれて、より高度な機能や管理タスクにも挑戦できるようになるでしょう。
