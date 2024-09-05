# SQL*Plus 使用時の注意点

SQL*Plusは強力なツールですが、使用する際には以下の点に注意が必要です。

## 1. セキュリティ

- **パスワードの取り扱い**: コマンドラインでパスワードを入力する際、画面に表示されることがあります。セキュアな接続方法を使用しましょう。

  例：パスワードを非表示にする
  ```
  sqlplus /nolog
  SQL> CONNECT username@database
  Enter password: 
  ```

- **権限管理**: 必要最小限の権限でログインしましょう。SYSDBAなどの高権限ユーザーでの接続は必要な時のみにしてください。

## 2. データ整合性

- **コミットの忘れ**: DML操作（INSERT, UPDATE, DELETE）後、COMMITを忘れずに実行しましょう。

  例：
  ```sql
  SQL> UPDATE employees SET salary = salary * 1.1;
  SQL> COMMIT;
  ```

- **ロールバック**: 誤った操作をした場合、ROLLBACKで取り消せます。

  例：
  ```sql
  SQL> DELETE FROM employees;  -- 誤って全削除してしまった！
  SQL> ROLLBACK;  -- 安全に取り消せる
  ```

## 3. パフォーマンス

- **大量データの取り扱い**: 大量のデータを扱う場合、メモリ消費に注意が必要です。

  例：結果を制限する
  ```sql
  SQL> SELECT * FROM large_table WHERE ROWNUM <= 1000;
  ```

- **長時間クエリ**: 実行時間の長いクエリは、システム全体に影響を与える可能性があります。

## 4. 出力の制御

- **PAGESIZE設定**: 大量の出力がある場合、PAGESIZEを適切に設定しないと、結果が画面をスクロールしてしまいます。

  例：
  ```
  SQL> SET PAGESIZE 50
  ```

- **LINESIZE設定**: 行が長すぎると折り返されて読みにくくなります。

  例：
  ```
  SQL> SET LINESIZE 100
  ```

## 5. スクリプトの取り扱い

- **エラー処理**: スクリプト内でエラーが発生した場合の処理を適切に行いましょう。

  例：エラー時に停止するスクリプト
  ```sql
  WHENEVER SQLERROR EXIT SQL.SQLCODE
  ```

- **コメント**: スクリプトには適切なコメントを入れ、後で見返しても理解できるようにしましょう。

  例：
  ```sql
  -- この処理は月次売上を計算します
  SELECT SUM(amount) FROM sales WHERE TRUNC(sale_date, 'MM') = TRUNC(SYSDATE, 'MM');
  ```

これらの注意点を意識しながらSQL*Plusを使用することで、より安全で効率的なデータベース操作が可能になります。初心者の方は特に、データの変更を行う前に必ずバックアップを取ることをお勧めします。
