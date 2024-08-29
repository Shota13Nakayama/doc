
# Oracle Data Pumpとディレクトリオブジェクト

## ディレクトリオブジェクトとは
ディレクトリオブジェクトは、Oracleデータベース内で物理的なOSディレクトリを表す論理的な構造です。
Data Pumpはこれを使用してダンプファイルの場所を指定します。
## 作成方法
```sql
CREATE DIRECTORY data_pump_dir AS '/u01/app/oracle/admin/orcl/dpdump';
```

## 権限付与
```sql
GRANT READ, WRITE ON DIRECTORY data_pump_dir TO hr;
```

## Data Pumpでの使用
エクスポート例:
```
expdp hr/password DIRECTORY=data_pump_dir DUMPFILE=export.dmp
```

インポート例:
```
impdp hr/password DIRECTORY=data_pump_dir DUMPFILE=export.dmp
```

## 注意点
- ディレクトリオブジェクトはデータベース内の論理名であり、実際のOSパスではありません
- Data Pump操作はサーバー側で実行されるため、クライアント側のパスは使用できません
- 適切な権限がないとData Pump操作が失敗します

ディレクトリオブジェクトを正しく設定することで、Data Pumpはセキュアかつ効率的にファイルにアクセスできます。

