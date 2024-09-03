# 環境変数 - 使用方法

## 1. 環境変数の表示

すべての環境変数を表示:
```
env
```

特定の環境変数の値を表示:
```
echo $VARIABLE_NAME
```

例:
```
echo $PATH
echo $HOME
```

## 2. 環境変数の設定

### 一時的な設定（現在のセッションのみであることに注意）

```
export VARIABLE_NAME=value
```

例:
```
export MY_VAR="Hello, World!"
```

### 永続的な設定

ユーザー固有の設定（~/.bashrc または ~/.bash_profile に追加）:
```
echo 'export VARIABLE_NAME=value' >> ~/.bashrc
```

システム全体の設定（/etc/environment に追加、要root権限）:
```
sudo echo 'VARIABLE_NAME=value' >> /etc/environment
```

## 3. 環境変数の削除

```
unset VARIABLE_NAME
```

## 4. PATH環境変数の操作

新しいパスを追加:
```
export PATH=$PATH:/new/path
```

## 5. 環境変数の使用

シェルスクリプトでの使用:
```bash
#!/bin/bash
echo "Hello, $USER!"
echo "Your home directory is $HOME"
```

コマンドラインでの使用:
```
cd $HOME
```

## 6. 条件付き環境変数の設定

値が未設定の場合のみ設定:
```
export VARIABLE_NAME=${VARIABLE_NAME:-default_value}
```

## 7. 環境変数の一覧表示とフィルタリング

特定のプレフィックスを持つ環境変数のみ表示:
```
env | grep ^PREFIX
```

例:
```
env | grep ^PATH
```

## 8. 子プロセスへの環境変数の受け渡し

```
VARIABLE_NAME=value command_to_run
```

例:
```
DEBUG=true ./my_script.sh
```

## 9. 設定の再読み込み

.bashrcファイルを編集後、変更を現在のセッションに適用:
```
source ~/.bashrc
```

これらの方法を使用して、環境変数を効果的に管理し、システムやアプリケーションの動作をカスタマイズすることができます。
