# Oracle-User-Rolesの使い方ガイド

Oracle-User-Rolesを初めて利用する方のために、以下に具体的なステップバイステップの使用方法を説明します。このガイドでは、ユーザーとロールの作成、ロールの付与、そして権限の管理について詳しく説明します。

## ユーザーの作成

1. **SQL*Plusに接続**
   ```sql
   sqlplus sys as sysdba
   ```

2. **新しいユーザーを作成**
   ```sql
   CREATE USER sample_user IDENTIFIED BY password;
   ```

3. **基本的な権限を付与**
   ```sql
   GRANT CREATE SESSION TO sample_user;
   ```

## ロールの作成

1. **新しいロールを作成**
   ```sql
   CREATE ROLE sample_role;
   ```

2. **ロールに権限を付与**
   ```sql
   GRANT CREATE TABLE TO sample_role;
   GRANT SELECT ANY TABLE TO sample_role;
   ```

## ロールのユーザーへの付与

1. **ユーザーにロールを付与**
   ```sql
   GRANT sample_role TO sample_user;
   ```

## 付与したロールの確認

1. **ユーザーが持っているロールを確認**
   ```sql
   SELECT * FROM DBA_ROLE_PRIVS WHERE GRANTEE = 'SAMPLE_USER';
   ```

## ロールの削除

1. **ロールを削除**
   ```sql
   DROP ROLE sample_role;
   ```

## まとめ

- **ユーザー作成**: 新しいユーザーを作成し、基本的なセッション権限を付与します。
- **ロール作成**: 必要な権限を持つロールを作成します。
- **ロール付与**: 作成したロールをユーザーに付与して、権限を管理します。
- **確認**: 付与したロールや権限を確認して、適切に管理されていることを確認します。

このガイドを参考にして、Oracle-User-Rolesを効果的に活用してください。