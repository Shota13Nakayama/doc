# 初心者のためのTCPDUMPガイド：SaaSとの通信を監視する方法

## 概要
このガイドでは、TCPDUMPを使用してSaaSアプリケーションとの間のHTTP/HTTPS通信を監視し、リクエストとレスポンスの内容（電文）を確認する方法を説明します。

## 準備

1. **TCPDUMPのインストール**（まだの場合）:
   ```
   sudo apt-get install tcpdump  # Ubuntuの場合
   sudo yum install tcpdump      # CentOSの場合
   ```

2. **SaaSアプリケーションのドメイン名を確認**:
   - 例: `example-saas.com`

3. **使用するネットワークインターフェースの確認**:
   ```
   ip addr
   ```
   - 通常、`eth0`や`ens33`などの名前です。以下では`eth0`と仮定します。

## 手順

### 1. 基本的な監視と電文の確認

```
sudo tcpdump -i eth0 host example-saas.com -A
```

- `-i eth0`: 監視するネットワークインターフェースを指定
- `host example-saas.com`: SaaSのドメイン名を指定
- `-A`: ASCII形式でパケットの内容（電文）を表示

### 電文の見方

TCPDUMPの出力では、各パケットが以下のような形式で表示されます：

```
時刻 IPプロトコル 送信元IP.ポート > 宛先IP.ポート: TCPフラグ
    電文の内容（HTTPヘッダーやボディ）
```

### HTTPリクエストのサンプルと解説

以下は、TCPDUMPで捉えられる典型的なHTTPリクエストのサンプルです：

```
12:34:56.789012 IP 192.168.1.100.54321 > 93.184.216.34.80: TCP 1234567:1234890(323) ACK 8901234 win 65535
GET /api/users HTTP/1.1
Host: example-saas.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
Accept: application/json
Accept-Language: en-US,en;q=0.9
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

```

このサンプルの各部分の意味：

1. **タイムスタンプと接続情報**:
   `12:34:56.789012 IP 192.168.1.100.54321 > 93.184.216.34.80: TCP 1234567:1234890(323) ACK 8901234 win 65535`
   - `12:34:56.789012`: パケットがキャプチャされた時刻
   - `192.168.1.100.54321`: 送信元IPアドレスとポート
   - `93.184.216.34.80`: 宛先IPアドレスとポート（80はHTTP）
   - `TCP 1234567:1234890(323)`: TCPシーケンス番号と送信バイト数
   - `ACK 8901234 win 65535`: TCP確認応答と受信ウィンドウサイズ

2. **HTTPリクエストライン**:
   `GET /api/users HTTP/1.1`
   - `GET`: HTTPメソッド（他にPOST、PUT、DELETEなどがある）
   - `/api/users`: リクエストのパス
   - `HTTP/1.1`: HTTPのバージョン

3. **HTTPヘッダー**:
   - `Host: example-saas.com`: リクエスト先のサーバー名
   - `User-Agent: ...`: クライアントのブラウザや環境情報
   - `Accept: application/json`: クライアントが受け入れるコンテンツタイプ
   - `Accept-Language: en-US,en;q=0.9`: クライアントが希望する言語
   - `Accept-Encoding: gzip, deflate, br`: クライアントがサポートする圧縮方式
   - `Connection: keep-alive`: 接続を維持するリクエスト

4. **リクエストボディ**:
   このサンプルではリクエストボディがありません。POSTリクエストの場合、ここにデータが含まれます。

### 2. HTTPヘッダーのみを表示（見やすくする）

```
sudo tcpdump -i eth0 host example-saas.com -A | grep -E "^(GET|POST|PUT|DELETE|PATCH|HTTP)"
```

これにより、HTTPメソッドとレスポンスステータスラインのみが表示され、電文の主要部分を簡単に確認できます。

### 3. パケットをファイルに保存して後で分析

```
sudo tcpdump -i eth0 host example-saas.com -w saas_traffic.pcap
```

保存したファイルを後で分析:

```
sudo tcpdump -r saas_traffic.pcap -A
```

## HTTPSの注意点

- HTTPS通信は暗号化されているため、TCPDUMPで見える内容は限定的です。
- 暗号化されたパケットでは、接続の確立や切断、パケットのサイズなどの情報は見えますが、実際の通信内容（HTTPヘッダーやボディ）は読み取れません。
- HTTPSの内容を確認するには、別途SSL/TLS復号化ツールが必要になります。

## 注意点

1. **プライバシーとセキュリティ**: キャプチャしたデータには機密情報が含まれている可能性があります。適切に取り扱ってください。
2. **パフォーマンス**: 大量のトラフィックをキャプチャすると、システムのパフォーマンスに影響を与える可能性があります。
3. **法的考慮**: 業務でこのツールを使用する場合、適切な許可を得てください。

## まとめ

TCPDUMPを使用することで、SaaSとの通信の電文（リクエストとレスポンス）を監視できます。HTTP通信の場合は内容を直接確認できますが、HTTPS通信の場合は暗号化のため内容を読み取ることはできません。このツールは、ネットワークレベルでの動作を理解したり、問題を診断したりするのに役立ちます。
