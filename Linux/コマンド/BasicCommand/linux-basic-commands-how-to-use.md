# Linux基本コマンド - 使い方ガイド

## 1. ファイルシステムナビゲーション

### pwd (Print Working Directory)
現在の作業ディレクトリを表示します。
```
pwd
```

### ls (List)
ディレクトリの内容をリスト表示します。
```
ls                # 基本的なリスト表示
ls -l             # 詳細な情報を表示
ls -a             # 隠しファイルを含むすべてのファイルを表示
ls -lh            # ファイルサイズを人間が読みやすい形式で表示
ls -R             # サブディレクトリの内容も再帰的に表示
```

### cd (Change Directory)
ディレクトリを変更します。
```
cd /path/to/directory  # 指定したディレクトリに移動
cd ..                  # 親ディレクトリに移動
cd ~                   # ホームディレクトリに移動
cd -                   # 直前のディレクトリに戻る
```

### tree
ディレクトリ構造をツリー形式で表示します。
```
tree                   # カレントディレクトリの構造を表示
tree -L 2              # 深さ2レベルまでの構造を表示
tree -d                # ディレクトリのみ表示
```
注: treeコマンドがインストールされていない場合は、`sudo apt-get install tree`（Debian/Ubuntu）または`sudo yum install tree`（CentOS/RHEL）でインストールできます。

## 2. ファイル操作

### touch
新しい空のファイルを作成するか、既存のファイルのタイムスタンプを更新します。
```
touch newfile.txt      # 新しいファイルを作成
touch -t 202301011200 file.txt  # ファイルのタイムスタンプを設定
```

### cp (Copy)
ファイルやディレクトリをコピーします。
```
cp source.txt destination.txt   # ファイルをコピー
cp -r sourcedir/ destdir/       # ディレクトリを再帰的にコピー
cp -i file.txt newlocation/     # 上書き前に確認
```

### mv (Move)
ファイルやディレクトリを移動または名前変更します。
```
mv oldname.txt newname.txt      # ファイル名を変更
mv file.txt /path/to/newlocation/  # ファイルを移動
mv -i sourcefile destfile       # 上書き前に確認
```

### rm (Remove)
ファイルやディレクトリを削除します。
```
rm file.txt            # ファイルを削除
rm -r directory/       # ディレクトリを再帰的に削除
rm -i file.txt         # 削除前に確認
rm -f file.txt         # 強制的に削除（確認なし）
```

### ln (Link)
ハードリンクまたはシンボリックリンクを作成します。
```
ln file.txt hardlink     # ハードリンクを作成
ln -s file.txt symlink   # シンボリックリンクを作成
```

## 3. ディレクトリ操作

### mkdir (Make Directory)
新しいディレクトリを作成します。
```
mkdir newdir            # 新しいディレクトリを作成
mkdir -p path/to/newdir # 必要に応じて親ディレクトリも作成
```

### rmdir (Remove Directory)
空のディレクトリを削除します。
```
rmdir emptydir          # 空のディレクトリを削除
```

## 4. ファイル内容の表示と編集

### cat (Concatenate)
ファイルの内容を表示します。
```
cat file.txt            # ファイルの内容を表示
cat file1.txt file2.txt # 複数ファイルの内容を連結して表示
cat > newfile.txt       # 新しいファイルを作成し、内容を入力（Ctrl+Dで終了）
```

### less
ファイルの内容をページングして表示します。
```
less largefile.txt
```
less内での操作:
- スペース: 次のページ
- b: 前のページ
- /: 検索
- n: 次の検索結果
- q: 終了

### head
ファイルの先頭部分を表示します。
```
head file.txt           # デフォルトで先頭10行を表示
head -n 20 file.txt     # 先頭20行を表示
```

### tail
ファイルの末尾部分を表示します。
```
tail file.txt           # デフォルトで末尾10行を表示
tail -n 20 file.txt     # 末尾20行を表示
tail -f logfile.txt     # ファイルの更新をリアルタイムで表示
```

### nano
シンプルなテキストエディタを起動します。
```
nano file.txt
```
nano内での基本操作:
- Ctrl+O: 保存
- Ctrl+X: 終了
- Ctrl+K: 行を切り取り
- Ctrl+U: 切り取った行を貼り付け

### vim
高度なテキストエディタを起動します。
```
vim file.txt
```
vim の基本操作:
- i: 挿入モード
- Esc: ノーマルモード
- :w: 保存
- :q: 終了
- :wq: 保存して終了
- /: 検索
- dd: 行を削除

## 5. ファイルの検索とテキスト処理

### grep (Global Regular Expression Print)
ファイル内の文字列を検索します。
```
grep "search term" file.txt     # ファイル内で"search term"を検索
grep -i "case insensitive" file.txt  # 大文字小文字を区別せずに検索
grep -r "term" directory/       # ディレクトリ内を再帰的に検索
grep -v "exclude" file.txt      # "exclude"を含まない行を表示
```

### find
ファイルやディレクトリを検索します。
```
find /path -name "*.txt"        # 指定パス以下で.txtファイルを検索
find . -type d                  # カレントディレクトリ以下のディレクトリを検索
find . -size +1M                # 1MB以上のファイルを検索
```

### awk
テキスト処理ツールです。
```
awk '{print $1}' file.txt       # 各行の第1フィールドを表示
awk -F: '{print $1}' /etc/passwd  # :で区切られたファイルの第1フィールドを表示
```

### sed (Stream Editor)
テキストの変換や置換を行います。
```
sed 's/old/new/' file.txt       # 'old'を'new'に置換（各行の最初の出現のみ）
sed 's/old/new/g' file.txt      # 'old'を'new'に置換（すべての出現）
```

## 6. システム情報とモニタリング

### uname
システム情報を表示します。
```
uname -a                # すべてのシステム情報を表示
uname -s                # カーネル名を表示
uname -r                # カーネルリリース番号を表示
```

### df (Disk Free)
ディスク使用量を表示します。
```
df -h                   # 人間が読みやすい形式で表示
df -i                   # iノード情報を表示
```

### free
メモリ使用量を表示します。
```
free -h                 # 人間が読みやすい形式で表示
free -s 5               # 5秒ごとに更新して表示
```

### top / htop
システムのリアルタイムモニタリングを行います。
```
top
htop                    # より高機能なtop（要インストール）
```
top/htop内での操作:
- q: 終了
- k: プロセスを終了
- r: プロセスの優先度を変更

## 7. プロセス管理

### ps (Process Status)
実行中のプロセスを表示します。
```
ps                      # 現在のシェルに関連するプロセスを表示
ps aux                  # システム全体のプロセスを詳細に表示
ps -ef                  # 完全なフォーマットでプロセスを表示
```

### kill
プロセスを終了します。
```
kill PID                # 指定したPIDのプロセスを終了
kill -9 PID             # 強制的にプロセスを終了
```

### jobs
バックグラウンドジョブを表示します。
```
jobs                    # バックグラウンドジョブのリストを表示
```

### bg (Background)
ジョブをバックグラウンドで実行します。
```
bg %job_number          # 指定したジョブをバックグラウンドで再開
```

### fg (Foreground)
バックグラウンドジョブをフォアグラウンドに移動します。
```
fg %job_number          # 指定したジョブをフォアグラウンドに移動
```

## 8. ネットワーク関連コマンド

### ping
ネットワーク接続をテストします。
```
ping google.com         # google.comへの接続をテスト
ping -c 4 192.168.1.1   # 4回だけpingを送信
```

### ifconfig / ip
ネットワークインターフェース情報を表示します。
```
ifconfig                # すべてのネットワークインターフェースを表示
ip addr show            # IPアドレス情報を表示（新しいコマンド）
```

### netstat
ネットワーク接続、ルーティングテーブル、インターフェース統計を表示します。
```
netstat -tuln           # アクティブな接続を表示
netstat -r              # ルーティングテーブルを表示
```

### ssh (Secure Shell)
リモートサーバーに安全に接続します。
```
ssh username@remote_host    # リモートホストに接続
ssh -p 2222 username@remote_host  # 特定のポートを指定して接続
```

## 9. パーミッションと所有権

### chmod (Change Mode)
ファイルのパーミッションを変更します。
```
chmod 755 file.txt      # ファイルに実行権限を付与
chmod u+x script.sh     # 所有者に実行権限を追加
chmod go-w file.txt     # グループとその他からの書き込み権限を削除
```

### chown (Change Owner)
ファイルの所有者を変更します。
```
chown user:group file.txt  # 所有者とグループを変更
chown -R user directory/   # ディレクトリを再帰的に所有者変更
```

### sudo (Superuser Do)
管理者権限でコマンドを実行します。
```
sudo command            # 指定したコマンドを管理者権限で実行
sudo -i                 # rootユーザーとしてシェルを開始
```

## 10. アーカイブとファイル圧縮

### tar (Tape Archive)
アーカイブの作成と展開を行います。
```
tar -cvf archive.tar files/  # アーカイブを作成
tar -xvf archive.tar         # アーカイブを展開
tar -czvf archive.tar.gz files/  # gzipで圧縮してアーカイブを作成
tar -xzvf archive.tar.gz     # gzip圧縮されたアーカイブを展開
```

### gzip / gunzip
ファイルの圧縮と解凍を行います。
```
gzip file.txt           # file.txtを圧縮してfile.txt.gzを作成
gunzip file.txt.gz      # file.txt.gzを解凍
```

## 11. パイプとリダイレクト

### パイプ (|)
コマンドの出力を別のコマンドの入力にします。
```
ls -l | grep ".txt"     # .txtファイルのみをリスト表示
ps aux | grep nginx     # nginxプロセスを検索
```

### リダイレクト (>, >>)
コマンドの出力をファイルに書き込みます。
```
echo "Hello" > file.txt  # ファイルに書き込み（上書き）
echo "World" >> file.txt # ファイルに追記
```

## 12. ヘルプとマニュアル

### man (Manual)
コマンドのマニュアルページを表示します。
```
man ls                  # lsコマンドのマニュアルを表示
man -k keyword          # キーワードに関連するマニュアルページを検索
```

### --help
コマンドのヘルプ情報を表示します。
```
ls --help               # lsコマンドのヘルプを表示
```

### info
詳細なドキュメントを表示します。
```
info coreutils          # GNU Coreutilsの詳細情報を表示
```

これらのコマンドを理解し、実践することで、Linuxシステムを効率的に操作できるようになります。コマンドの詳細なオプションや使用例については、各コマンドのマニュアルページ（man）を参照することをお勧めします。
