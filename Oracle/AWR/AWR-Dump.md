https://www.ashisuto.co.jp/db_blog/article/oracle_awrextr-sql.html

# awrextr.sql
AWRのデータをダンプファイルとして出力できる。
つまり、レポートを1時間単位で５つください！のようなやりとりはいらない。


# AWRスナップショットのエクスポート手順

AWRのスナップショットデータをダンプファイルとしてエクスポートする手順を以下に示します。

## 手順

1. SQL*Plusに SYS ユーザーで接続します。

2. 次のコマンドを実行して awrextr.sql スクリプトを起動します:
```sql
SQL> @$ORACLE_HOME/rdbms/admin/awrextr.sql
```

3. データベースIDを入力するよう求められるので、対象のデータベースIDを入力します。

4. スナップショットIDの一覧を表示する日数を入力します。

5. エクスポートする範囲の開始スナップショットIDと終了スナップショットIDを入力します。

6. ダンプファイルを格納するディレクトリを指定します。

7. ダンプファイル名を入力します(拡張子は不要)。

## サンプル実行例

以下は実行例です：

```sql
SQL> @$ORACLE_HOME/rdbms/admin/awrextr.sql

Specify the Database Id (DBID) for the PDB or CDB: 1234567890
Using 1234567890 for database Id

Specify the number of days of snapshots to choose from
Enter value for num_days: 2

Specify the Begin and End Snapshot Ids
Enter value for begin_snap: 30
Enter value for end_snap: 40

Specify the Degree of Parallelism
Enter value for degree: 1

Specify the Output Directory
Enter value for directory_name: DATA_PUMP_DIR

Specify the File Name
Enter value for file_name: my_awr_dump

```

この例では、データベースID 1234567890 の過去2日間のスナップショットから、
スナップショットID 30 から 40 までのデータを "my_awr_dump.dmp" というファイル名で
DATA_PUMP_DIR ディレクトリにエクスポートしています。

エクスポートが完了すると、指定したディレクトリにダンプファイルが作成されます。
このファイルは後で別のデータベースにインポートすることができます。

## AWRダンプの注意点

1. **ダンプファイルのサイズ**:
   AWRダンプファイルは非常に大きくなる可能性があります。特に以下の場合はサイズが大きくなります：
   - 長期間のデータをエクスポートする場合
   - 大規模なデータベースの場合
   - アクティビティが多いデータベースの場合

   十分なディスク容量があることを確認してください。

2. **エクスポート時間**:
   大量のデータをエクスポートする場合、処理に時間がかかることがあります。
   システムへの影響を最小限に抑えるため、できるだけ負荷の少ない時間帯に実行することをおすすめします。

3. **パフォーマンスへの影響**:
   エクスポート処理中はシステムリソースを消費するため、本番環境での実行には注意が必要です。
   可能であれば、メンテナンス時間中や負荷の少ない時間帯に実行してください。

4. **セキュリティ**:
   AWRダンプには機密情報が含まれる可能性があります。
   ダンプファイルは安全に保管し、必要に応じてアクセス制限を設けてください。

5. **バージョン互換性**:
   AWRダンプをインポートする際は、エクスポート元とインポート先のOracleバージョンの互換性に注意してください。
   異なるバージョン間でのインポートは問題が発生する可能性があります。

6. **スナップショット範囲の選択**:
   必要最小限のスナップショット範囲を選択することで、ダンプファイルのサイズを抑え、
   処理時間を短縮できます。目的に応じて適切な範囲を選択してください。

これらの点に注意しながらAWRダンプのエクスポートを行うことで、
より効率的かつ安全にデータを取得することができます。

