# Yum: 使用方法

Yumを使用してパッケージを管理する基本的な方法を以下に示します：

1. **パッケージのインストール**:
   ```
   sudo yum install package_name
   ```
   複数のパッケージを同時にインストールする場合：
   ```
   sudo yum install package1 package2 package3
   ```

2. **パッケージの更新**:
   特定のパッケージを更新：
   ```
   sudo yum update package_name
   ```
   システム全体を更新：
   ```
   sudo yum update
   ```

3. **パッケージの削除**:
   ```
   sudo yum remove package_name
   ```

4. **パッケージの検索**:
   ```
   yum search keyword
   ```

5. **パッケージ情報の表示**:
   ```
   yum info package_name
   ```

6. **インストール済みパッケージの一覧表示**:
   ```
   yum list installed
   ```

7. **利用可能な更新の確認**:
   ```
   yum check-update
   ```

8. **リポジトリの一覧表示**:
   ```
   yum repolist
   ```

9. **キャッシュのクリア**:
   ```
   sudo yum clean all
   ```

10. **グループパッケージの管理**:
    グループの一覧表示：
    ```
    yum grouplist
    ```
    グループのインストール：
    ```
    sudo yum groupinstall "Group Name"
    ```

11. **特定のバージョンのパッケージをインストール**:
    ```
    sudo yum install package_name-version
    ```

12. **依存関係の表示**:
    ```
    yum deplist package_name
    ```

13. **Yumのヒストリーの表示**:
    ```
    yum history
    ```

14. **ダウングレード**:
    ```
    sudo yum downgrade package_name
    ```

これらのコマンドを使用することで、Yumを通じてシステムのパッケージを効果的に管理できます。より詳細な情報が必要な場合は、`man yum` コマンドでマニュアルを参照できます。
