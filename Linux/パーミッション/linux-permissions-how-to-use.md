# Linuxパーミッション - 使用方法（ファイルとディレクトリ）

ファイルとディレクトリのパーミッションの表示、変更、および管理方法について説明します。

## パーミッションの表示

### ls コマンドを使用
```
ls -l filename
ls -ld directoryname
```
出力例: `-rwxr-xr-x 1 user group 4096 Jan 1 12:00 filename`

先頭の文字は、ファイルタイプを示します：
- `-`: 通常のファイル
- `d`: ディレクトリ
- `l`: シンボリックリンク

## パーミッションの変更

### chmod コマンド

1. シンボリック表記:
   ```
   chmod u+x filename     # 所有者に実行権限を追加
   chmod g-w directoryname  # グループから書き込み権限を削除
   chmod o=r filename     # その他に読み取り権限のみを設定
   ```

2. 数値表記:
   ```
   chmod 755 filename     # rwxr-xr-x に設定
   chmod 644 filename     # rw-r--r-- に設定
   chmod 700 directoryname  # rwx------ に設定（所有者のみフルアクセス）
   ```

3. 再帰的に変更:
   ```
   chmod -R 755 directoryname  # ディレクトリとその中身全てに適用
   ```

## ディレクトリ特有の設定例

1. ディレクトリ内のファイル一覧表示を許可、但しアクセスは禁止:
   ```
   chmod 711 directoryname
   ```

2. グループメンバーにフルアクセス権を与え、その他には読み取りと実行のみ許可:
   ```
   chmod 775 directoryname
   ```

## 特殊なパーミッションの設定

### SetUID (ファイルのみ)
```
chmod u+s filename
```

### SetGID (ファイルとディレクトリ)
```
chmod g+s filename
chmod g+s directoryname  # ディレクトリ内に作成される新規ファイルにグループ継承
```

### Sticky Bit (主にディレクトリ)
```
chmod +t directoryname
```

## 所有者とグループの変更

### chown コマンド
```
chown newowner filename
chown newowner:newgroup directoryname
chown -R newowner:newgroup directoryname  # 再帰的に変更
```

## パーミッションの確認と解釈

### アクセス可能か確認
```
test -r filename && echo "読み取り可能" || echo "読み取り不可"
test -w directoryname && echo "書き込み可能" || echo "書き込み不可"
test -x directoryname && echo "アクセス可能" || echo "アクセス不可"
```

### ファイルタイプとパーミッションの確認
```
ls -ld directoryname  # ディレクトリの場合
ls -l filename        # 通常のファイルの場合
```

これらのコマンドを使用して、Linuxシステム上でファイルとディレクトリのパーミッションを効果的に管理できます。ディレクトリのパーミッションがそのディレクトリ内のファイルへのアクセスに大きく影響することを常に意識してください。
