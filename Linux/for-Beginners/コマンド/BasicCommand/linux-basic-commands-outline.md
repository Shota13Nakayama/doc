# Linux基本コマンド - アウトライン
## 1. ファイルシステムナビゲーション
- pwd：現在の作業ディレクトリを表示
- ls：ディレクトリの内容をリスト表示
- cd：ディレクトリを変更
- tree：ディレクトリ構造を表示（要インストール）

## 2. ファイル操作
- touch：新しいファイルを作成
- cp：ファイルやディレクトリをコピー
- mv：ファイルやディレクトリを移動または名前変更
- rm：ファイルやディレクトリを削除
- ln：ハードリンクとシンボリックリンクの作成

## 3. ディレクトリ操作
- mkdir：新しいディレクトリを作成
- rmdir：空のディレクトリを削除

## 4. ファイル内容の表示と編集
- cat：ファイルの内容を表示
- less：ファイルの内容をページングして表示
- head/tail：ファイルの先頭/末尾を表示
- nano：シンプルなテキストエディタ
- vim：高度なテキストエディタ（基本操作）

## 5. ファイルの検索とテキスト処理
- grep：ファイル内の文字列検索
- find：ファイルやディレクトリの検索
- awk/sed：テキスト処理ツール（基本的な使用方法）

## 6. システム情報とモニタリング
- uname：システム情報を表示
- df：ディスク使用量を表示
- free：メモリ使用量を表示
- top/htop：システムのリアルタイムモニタリング

## 7. プロセス管理
- ps：実行中のプロセスを表示
- kill：プロセスを終了
- jobs, bg, fg：ジョブ制御

## 8. ネットワーク関連コマンド
- ping：ネットワーク接続のテスト
- ifconfig/ip：ネットワークインターフェース情報
- netstat：ネットワーク統計
- ssh：リモートサーバーへの安全な接続

## 9. パーミッションと所有権
- chmod：ファイルのパーミッションを変更
- chown：ファイルの所有者を変更
- sudo：管理者権限でコマンドを実行

## 10. アーカイブとファイル圧縮
- tar：アーカイブの作成と展開
- gzip/gunzip：ファイルの圧縮と解凍

## 11. パイプとリダイレクト
- |（パイプ）：コマンドの出力を別のコマンドの入力にする
- >、>>（リダイレクト）：出力をファイルに書き込む

## 12. ヘルプとマニュアル
- man：コマンドのマニュアルページを表示
- --help：コマンドのヘルプ情報を表示
- info：詳細なドキュメントを表示
