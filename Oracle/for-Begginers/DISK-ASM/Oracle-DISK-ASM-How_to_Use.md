# Oracle-DISK-ASM 使い方ガイド

## はじめに
Oracle-DISK-ASM（Automatic Storage Management）は、Oracleデータベースのストレージ管理を簡素化するためのツールです。このガイドでは、Oracle-DISK-ASMを初めて使用する方向けに具体的な手順を提供します。

## 前提条件
- Oracle Databaseがインストールされていること
- ASMインスタンスが作成されていること
- 管理者権限があること

## 手順

### 1. ASMディスクグループの作成
最初に、ASMディスクグループを作成します。ディスクグループは、データベースのデータを格納するための論理的なストレージ単位です。

#### コマンド例:
```sql
CREATE DISKGROUP data_disk_group EXTERNAL REDUNDANCY DISK '/dev/oracleasm/disks/DISK1';
```

### 2. ASMディスクの追加
新しいディスクを追加して、ディスクグループを拡張することができます。

#### コマンド例:
```sql
ALTER DISKGROUP data_disk_group ADD DISK '/dev/oracleasm/disks/DISK2';
```

### 3. ASMディスクの削除
不要になったディスクを削除することも可能です。

#### コマンド例:
```sql
ALTER DISKGROUP data_disk_group DROP DISK DISK2;
```

### 4. ディスクグループの監視
ディスクグループの状態を監視するためのコマンドもいくつかあります。

#### コマンド例:
```sql
SELECT name, state FROM v$asm_diskgroup;
```

### 5. ディスクグループのリバランス
ディスクの追加や削除後、ディスクグループのリバランスを実行することで、データの分散を最適化します。

#### コマンド例:
```sql
ALTER DISKGROUP data_disk_group REBALANCE POWER 4;
```

## まとめ
以上の手順を通じて、ASMディスクグループの作成、管理、監視が簡単に行えるようになります。Oracle-DISK-ASMを活用することで、ストレージ管理が効率化され、データベースのパフォーマンスが向上します。

このガイドが、Oracle-DISK-ASMの利用を始める一助となれば幸いです。