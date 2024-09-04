# Yum: 使用方法

Yumを使用してパッケージを管理する基本的な方法を以下に示します。特に、ローカルリポジトリの使用方法に焦点を当てます。

## 1. 基本的なYumコマンド

1. **パッケージのインストール**:
   ```
   sudo yum install package_name
   ```

2. **パッケージの更新**:
   ```
   sudo yum update package_name
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

## 2. ローカルリポジトリの作成と使用

### ローカルリポジトリの作成

1. **必要なパッケージのダウンロード**:
   ```
   sudo yum install createrepo yum-utils
   ```

2. **リポジトリ用ディレクトリの作成**:
   ```
   sudo mkdir -p /var/www/html/localrepo
   ```

3. **必要なRPMパッケージのダウンロード**:
   ```
   sudo reposync -g -l -d -m --repoid=rhel-7-server-rpms --newest-only --download-metadata --download_path=/var/www/html/localrepo/
   ```

4. **リポジトリメタデータの作成**:
   ```
   sudo createrepo /var/www/html/localrepo/
   ```

### ローカルリポジトリの使用

1. **新しいリポジトリ設定ファイルの作成**:
   `/etc/yum.repos.d/localrepo.repo` ファイルを作成し、以下の内容を記述:

   ```
   [localrepo]
   name=Local Repository
   baseurl=file:///var/www/html/localrepo
   enabled=1
   gpgcheck=0
   ```

2. **Yumキャッシュのクリア**:
   ```
   sudo yum clean all
   ```

3. **リポジトリリストの確認**:
   ```
   yum repolist
   ```

4. **ローカルリポジトリからのパッケージインストール**:
   ```
   sudo yum install --disablerepo="*" --enablerepo="localrepo" package_name
   ```

## 3. その他の有用なコマンド

1. **特定のリポジトリからのみインストール**:
   ```
   sudo yum --disablerepo="*" --enablerepo="localrepo" install package_name
   ```

2. **リポジトリの優先度設定**:
   リポジトリの設定ファイルに `priority=1` を追加（数字が小さいほど優先度が高い）

3. **ローカルリポジトリの更新**:
   ```
   sudo reposync -g -l -d -m --repoid=rhel-7-server-rpms --newest-only --download-metadata --download_path=/var/www/html/localrepo/
   sudo createrepo --update /var/www/html/localrepo/
   ```

4. **ローカルRPMファイルからのインストール**:
   ```
   sudo yum localinstall /path/to/package.rpm
   ```

5. **依存関係の表示**:
   ```
   yum deplist package_name
   ```

これらのコマンドとローカルリポジトリの設定方法を使用することで、インターネットに接続されていない環境や、厳格なネットワークポリシーが適用されている環境でもYumを効果的に利用できます。ローカルリポジトリを使用することで、パッケージの管理とシステムの更新をより安全かつ効率的に行うことができます。
