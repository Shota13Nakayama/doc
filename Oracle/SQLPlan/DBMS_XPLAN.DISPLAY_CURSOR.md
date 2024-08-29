
DBMS_XPLAN.DISPLAY_CURSORは、共有プール内の現在のメモリ上のカーソルから実行計画を取得します。つまり、SQLがメモリ上に残っている必要があります。

# DBMS_XPLAN.DISPLAY_CURSORを使用した実行計画の取得

## 実行計画取得の条件

DBMS_XPLAN.DISPLAY_CURSORを使用して特定のSQL IDの実行計画を取得するための条件は以下の通りです：

SQLがメモリ上（共有プール内）に残っていること

## 説明

DBMS_XPLAN.DISPLAY_CURSORは、現在のメモリ（共有プール）内のカーソルから実行計画を取得します。そのため、対象のSQLがメモリ上に残っている必要があります。

AWRスナップショットの存在は、DBMS_XPLAN.DISPLAY_CURSORの使用条件ではありません。AWRは別の目的（長期的なパフォーマンス分析など）で使用されます。

## 注意点

- SQLがメモリから削除されている場合、DBMS_XPLAN.DISPLAY_CURSORでは実行計画を取得できません。
- 最近実行されたSQLや頻繁に実行されるSQLは、メモリ上に残っている可能性が高くなります。
- メモリ上にSQLが残っている時間は、データベースの設定や負荷状況によって異なります。

## 代替手段

メモリ上にSQLが残っていない場合、以下の方法で過去の実行計画を確認できる可能性があります：

1. DBMS_XPLAN.DISPLAY_AWR: AWRに保存された実行計画を表示
		→ https://docs.oracle.com/cd/E16338_01/appdev.112/b56262/d_xplan.htm
2. DBA_HIST_SQL_PLAN: AWRに保存された実行計画の履歴を確認

これらの方法を使用する場合は、AWRスナップショットが存在し、対象のSQLの情報が含まれている必要があります。

