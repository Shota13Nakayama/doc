# Oracle-Multitenant-CDB-PDBの使い方ガイド

## はじめに
このガイドでは、Oracle MultitenantのCDB（コンテナデータベース）およびPDB（プラガブルデータベース）を利用するための基本的な手順を初心者向けに説明します。具体的な操作方法や実用的なケースを中心に、わかりやすく解説します。

### 前提条件
以下の前提条件を満たしていることを確認してください。
- Oracle Databaseがインストールされていること。
- 管理者権限を持っていること。
- 基本的なSQL知識があること。

## ステップ1: CDBの作成

### 1. Oracle Database Configuration Assistant (DBCA)を使用
1. **DBCAを起動**: コマンドラインで`dbca`を実行します。
2. **データベースの作成**を選択。
3. **データベースのタイプ**として「コンテナデータベース（CDB）」を選択。
4. 必要な情報（データベース名、パスワード、保存場所など）を入力し、CDBを作成します。

### 2. SQL*Plusを使用
1. **SQL*Plusに接続**:
   ```sql
   sqlplus / as sysdba
   ```
2. **CDBの作成**:
   ```sql
   CREATE DATABASE cdb1
   USER SYS IDENTIFIED BY password
   USER SYSTEM IDENTIFIED BY password
   ENABLE PLUGGABLE DATABASE;
   ```

## ステップ2: PDBの作成

### 1. DBCAを使用
1. **DBCAを起動**: コマンドラインで`dbca`を実行します。
2. **プラガブルデータベースの管理**を選択。
3. **PDBの作成**を選択し、必要な情報を入力します。

### 2. SQL*Plusを使用
1. **SQL*Plusに接続**:
   ```sql
   sqlplus / as sysdba
   ```
2. **PDBの作成**:
   ```sql
   CREATE PLUGGABLE DATABASE pdb1
   ADMIN USER pdb_admin IDENTIFIED BY password
   FILE_NAME_CONVERT = ('/u01/app/oracle/oradata/cdb1/', '/u01/app/oracle/oradata/cdb1/pdb1/');
   ```
3. **PDBのオープン**:
   ```sql
   ALTER PLUGGABLE DATABASE pdb1 OPEN;
   ```

## ステップ3: PDBへの接続

### 1. SQL*Plusを使用
1. **SQL*Plusに接続**:
   ```sql
   sqlplus pdb_admin@pdb1
   ```
2. **PDBの確認**:
   ```sql
   SHOW CON_NAME;
   ```

## ステップ4: PDBの管理

### PDBの起動と停止
1. **PDBの起動**:
   ```sql
   ALTER PLUGGABLE DATABASE pdb1 OPEN;
   ```
2. **PDBの停止**:
   ```sql
   ALTER PLUGGABLE DATABASE pdb1 CLOSE IMMEDIATE;
   ```

### PDBのアンプラグと再プラグ
1. **PDBのアンプラグ**:
   ```sql
   ALTER PLUGGABLE DATABASE pdb1 UNPLUG INTO '/path/to/pdb1.xml';
   ```
2. **PDBの再プラグ**:
   ```sql
   CREATE PLUGGABLE DATABASE pdb1 USING '/path/to/pdb1.xml' COPY;
   ```

## まとめ
このガイドでは、Oracle MultitenantのCDBおよびPDBを利用するための基本的な手順を説明しました。これらの手順を実行することで、コンテナデータベースとプラガブルデータベースの作成、接続、管理ができるようになります。初心者の方でも理解しやすいように、具体的なコマンドと手順を示しましたので、実際に手を動かしながら学んでください。