# Oracle-Datapumpの使い方ガイド

Oracle-DatapumpはOracleデータベースのデータ移行ツールで、データベースのエクスポート（バックアップ）とインポート（リストア）を効率的に行うための機能を提供します。ここでは、初心者向けにOracle-Datapumpの基本的な使い方をステップバイステップで解説します。

## 1. 前提条件

Oracle-Datapumpを使用する前に、以下の前提条件を確認してください：

- Oracle Databaseがインストールされていること
- 使用するユーザーが適切な権限を持っていること（通常はDBA権限）

## 2. エクスポート（バックアップ）の手順

エクスポートとは、データベースの内容をダンプファイルとして保存するプロセスです。これにより、データベースのバックアップが取れます。

### 2.1 エクスポートの基本コマンド

以下は、簡単なエクスポートの例です：

```shell
expdp ユーザー名/パスワード@データベース名 schemas=スキーマ名 directory=ディレクトリ名 dumpfile=ファイル名.dmp logfile=ログファイル名.log
```

### 2.2 実行例

具体的なコマンドの例を見てみましょう：

```shell
expdp scott/tiger@orcl schemas=scott directory=DATA_PUMP_DIR dumpfile=scott_schema.dmp logfile=scott_export.log
```

このコマンドは、`scott` スキーマを `DATA_PUMP_DIR` ディレクトリに `scott_schema.dmp` というダンプファイルとしてエクスポートし、ログファイルは `scott_export.log` に出力します。

## 3. インポート（リストア）の手順

インポートとは、エクスポートされたダンプファイルを使用してデータベースにデータをリストアするプロセスです。

### 3.1 インポートの基本コマンド

以下は、簡単なインポートの例です：

```shell
impdp ユーザー名/パスワード@データベース名 schemas=スキーマ名 directory=ディレクトリ名 dumpfile=ファイル名.dmp logfile=ログファイル名.log
```

### 3.2 実行例

具体的なコマンドの例を見てみましょう：

```shell
impdp scott/tiger@orcl schemas=scott directory=DATA_PUMP_DIR dumpfile=scott_schema.dmp logfile=scott_import.log
```

このコマンドは、`scott_schema.dmp` ダンプファイルを使用して `scott` スキーマをリストアし、ログファイルは `scott_import.log` に出力します。

## 4. ディレクトリオブジェクトの作成

エクスポートやインポートの前に、ディレクトリオブジェクトを作成する必要があります。これは、Oracleデータベースがダンプファイルを読み書きするためのディレクトリを指定するものです。

### 4.1 ディレクトリオブジェクトの作成コマンド

```sql
CREATE DIRECTORY ディレクトリ名 AS 'パス';
GRANT READ, WRITE ON DIRECTORY ディレクトリ名 TO ユーザー名;
```

### 4.2 実行例

具体的なコマンドの例を見てみましょう：

```sql
CREATE DIRECTORY DATA_PUMP_DIR AS '/u01/app/oracle/oradata';
GRANT READ, WRITE ON DIRECTORY DATA_PUMP_DIR TO scott;
```

これにより、`/u01/app/oracle/oradata` ディレクトリへの読み書き権限が `scott` ユーザーに付与されます。

## 5. まとめ

Oracle-Datapumpを使用することで、データベースのエクスポートとインポートを効率的に行うことができます。基本的なコマンドとその使用方法を理解することで、データベース管理の初歩的な作業をスムーズに行うことができるようになります。まずは、簡単なエクスポートとインポートを試してみて、操作に慣れて