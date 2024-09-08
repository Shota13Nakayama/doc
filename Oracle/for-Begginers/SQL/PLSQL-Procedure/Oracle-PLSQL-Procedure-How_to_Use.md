# Oracle-PLSQL-Procedureの使い方ガイド

## はじめに
このガイドでは、Oracle-PLSQL-Procedureの基本的な使い方について説明します。手順ごとに分かりやすく解説しますので、初めての方でも安心して学べます。

## 1. PLSQLプロシージャの作成

### ステップ1: PLSQLプロシージャの基本構文
PLSQLプロシージャは、事前に定義された一連のSQL文とPLSQLブロックを実行するためのプログラム単位です。以下は基本的な構文です：

```sql
CREATE OR REPLACE PROCEDURE procedure_name
IS
BEGIN
    -- PL/SQL statements
END procedure_name;
```

### ステップ2: 簡単なプロシージャの例
例えば、「Hello, World!」を出力するプロシージャを作成しましょう。

```sql
CREATE OR REPLACE PROCEDURE say_hello
IS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Hello, World!');
END say_hello;
```

### ステップ3: プロシージャの実行
プロシージャを実行するには、以下のSQLコマンドを使用します：

```sql
BEGIN
    say_hello;
END;
```

## 2. パラメータ付きプロシージャ

### ステップ1: パラメータの追加
プロシージャにパラメータを追加することで、外部から値を受け取ることができます。以下はパラメータ付きプロシージャの例です：

```sql
CREATE OR REPLACE PROCEDURE greet_user(p_name IN VARCHAR2)
IS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Hello, ' || p_name || '!');
END greet_user;
```

### ステップ2: パラメータ付きプロシージャの実行
パラメータを指定してプロシージャを実行するには、以下のようにします：

```sql
BEGIN
    greet_user('Alice');
END;
```

## 3. エラーハンドリング

### ステップ1: EXCEPTIONセクションの追加
プロシージャ内でエラーが発生した場合に備えて、EXCEPTIONセクションを追加します。以下は例です：

```sql
CREATE OR REPLACE PROCEDURE divide_numbers(p_num1 IN NUMBER, p_num2 IN NUMBER)
IS
    v_result NUMBER;
BEGIN
    v_result := p_num1 / p_num2;
    DBMS_OUTPUT.PUT_LINE('Result: ' || v_result);
EXCEPTION
    WHEN ZERO_DIVIDE THEN
        DBMS_OUTPUT.PUT_LINE('Error: Division by zero is not allowed.');
END divide_numbers;
```

### ステップ2: エラーハンドリングの実行
エラーハンドリングを確認するために、ゼロで割る操作を実行します：

```sql
BEGIN
    divide_numbers(10, 0);
END;
```

## 4. 後片付け

### ステップ1: プロシージャの削除
不要になったプロシージャは削除することができます。以下のコマンドを使用します：

```sql
DROP PROCEDURE procedure_name;
```

例：

```sql
DROP PROCEDURE say_hello;
```

## まとめ
このガイドでは、Oracle-PLSQL-Procedureの基本的な使い方を紹介しました。プロシージャの作成、実行、パラメータの使用、エラーハンドリング、そしてプロシージャの削除について学びました。これを基に、さらに複雑なプロシージャを作成し、データベース操作を効率化してください。