# OracleRMANの使い方ガイド

## はじめに
OracleRMAN（Recovery Manager）は、Oracleデータベースのバックアップとリカバリを効率的に行うためのツールです。このガイドでは、OracleRMANを初めて使用する初心者向けに、基本的なステップと実用的な使用例を紹介します。

## 1. OracleRMANのインストールと設定

### 1.1 インストールの確認
Oracleデータベースをインストールすると、OracleRMANも自動的にインストールされます。以下のコマンドでインストールを確認できます。

```shell
$ rman
```

### 1.2 設定ファイルの準備
バックアップやリカバリをスムーズに行うための設定ファイルを用意します。以下は設定ファイルの一例です。

```shell
CONFIGURE RETENTION POLICY TO REDUNDANCY 2;
CONFIGURE BACKUP OPTIMIZATION ON;
CONFIGURE CONTROLFILE AUTOBACKUP ON;
```

## 2. バックアップの実行

### 2.1 データベース全体のバックアップ
OracleRMANを使用してデータベース全体をバックアップする基本的な方法は以下の通りです。

```shell
$ rman target /
RMAN> BACKUP DATABASE;
```

### 2.2 アーカイブログのバックアップ
アーカイブログをバックアップすることで、障害発生時にデータベースをより確実にリカバリできるようになります。

```shell
$ rman target /
RMAN> BACKUP ARCHIVELOG ALL;
```

## 3. リカバリの実行

### 3.1 データベース全体のリカバリ
以下のコマンドで、バックアップからデータベース全体をリカバリします。

```shell
$ rman target /
RMAN> RESTORE DATABASE;
RMAN> RECOVER DATABASE;
```

### 3.2 特定のテーブルスペースのリカバリ
特定のテーブルスペースのみをリカバリする場合は、以下の手順を実行します。

```shell
$ rman target /
RMAN> RESTORE TABLESPACE tablespace_name;
RMAN> RECOVER TABLESPACE tablespace_name;
```

## 4. バックアップの検証

### 4.1 バックアップの検証
バックアップが正常に行われたかどうかを確認するために、以下のコマンドを実行します。

```shell
$ rman target /
RMAN> VALIDATE BACKUPSET backupset_number;
```

## 5. OracleRMANのスクリプト化

### 5.1 スクリプトの作成
定期的なバックアップを自動化するために、スクリプトを作成します。以下はスクリプトの例です。

```shell
run {
  allocate channel c1 type disk;
  backup database;
  backup archivelog all;
  release channel c1;
}
```

### 5.2 スクリプトの実行
作成したスクリプトを実行するには、以下のコマンドを使用します。

```shell
$ rman target / @backup_script.rman
```

## まとめ
このガイドでは、OracleRMANを使用してデータベースのバックアップとリカバリを行う基本的な手順を紹介しました。これらのステップを実践することで、安全かつ効果的にデータベースの保護を行うことができます。