# Oracle RAC データベースアーキテクチャの使い方ガイド

## はじめに
このガイドでは、Oracle Real Application Clusters (RAC) データベースアーキテクチャを初心者向けに解説します。各ステップを順を追って説明していますので、基本的な技術的背景があれば、Oracle RACの実践的な使い方を理解できるようになります。

## 前提条件
- Oracle Databaseの基本的な知識
- Linux/Unixの基本操作
- ネットワークの基本知識

## 準備
### 必要なソフトウェアとハードウェア
- Oracle Database Enterprise Edition
- Oracle Clusterware
- 共有ストレージ (SAN/NAS)
- 複数のサーバー (通常は2つ以上)

### ネットワーク設定
Oracle RACは複数のインスタンス間でデータベースを共有します。そのため、次のネットワーク構成が必要です：
- **パブリックネットワーク:** クライアントアクセス用
- **プライベートネットワーク:** インターコネクト用（インスタンス間の通信）

## インストールと設定

### 1. 共有ストレージの設定
共有ストレージを設定し、各ノードからアクセスできるようにします。例として、SANストレージを使用する場合：
```bash
# 各ノードで共有ストレージをマウント
mount -t nfs <ストレージ_IP>:/shared_volume /mnt/shared
```

### 2. Oracle Clusterwareのインストール
Oracle Clusterwareを全ノードにインストールします。
```bash
# Oracle Grid Infrastructureソフトウェアのインストール
./gridSetup.sh
```
インストール中にクラスターネットワークの設定やノードの追加を行います。

### 3. データベースソフトウェアのインストール
Oracle Databaseソフトウェアを全ノードにインストールします。
```bash
# Oracle Databaseソフトウェアのインストール
./runInstaller
```

### 4. データベースの作成
Oracle RACデータベースを作成します。以下はOracle DBCA (Database Configuration Assistant)を使用した例です：
```bash
# DBCAを起動
dbca

# RACデータベースを作成
1. データベース操作モードで「RACデータベースの作成」を選択
2. 必要な設定を入力
```

### 5. インスタンスの追加
RACクラスタにインスタンスを追加します。
```bash
# インスタンスの追加
srvctl add instance -db <データベース名> -instance <インスタンス名> -node <ノード名>
```

## 使用例

### クライアント接続
クライアントからOracle RACデータベースに接続するには、TNS (Transparent Network Substrate) エントリを使用します。
```sql
# tnsnames.ora ファイルの設定例
RACDB =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = <ホスト名>)(PORT = 1521))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = racdb)
    )
  )
```
クライアントから接続：
```sql
sqlplus user/password@RACDB
```

### ファイルシステムの管理
Oracle RACでは、共有ストレージ上でデータファイルを管理します。例として、データファイルの追加：
```sql
ALTER TABLESPACE users ADD DATAFILE '/mnt/shared/datafile02.dbf' SIZE 100M;
```

## まとめ
Oracle RACデータベースアーキテクチャを理解し、実際に使用するための基本的な手順を説明しました。実際の運用では、より詳細な設定や監視が必要になる場合がありますが、まずはこのガイドを参考にして基礎を築いてください。