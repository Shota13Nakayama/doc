# 名前解決の使い方ガイド

名前解決は、コンピュータネットワークにおいて、人間が理解しやすい名前（例: www.example.com）をコンピュータが理解できるIPアドレス（例: 192.0.2.1）に変換するプロセスです。このガイドでは、初心者向けに名前解決を利用するためのステップバイステップの手順を説明します。

## ステップ 1: ドメイン名を理解する
ウェブサイトやネットワークリソースにアクセスする際には、ドメイン名を使用します。例として、ウェブブラウザのアドレスバーに「www.example.com」と入力します。

## ステップ 2: DNSサーバーの役割
DNS（Domain Name System）サーバーは、ドメイン名を対応するIPアドレスに変換する役割を果たします。通常、インターネットサービスプロバイダ（ISP）がデフォルトのDNSサーバーを提供しますが、Google Public DNS（8.8.8.8, 8.8.4.4）やCloudflare（1.1.1.1）などのパブリックDNSサーバーを使用することもできます。

## ステップ 3: DNS設定の確認と変更
### Windowsの場合
1. **コントロールパネル**を開きます。
2. **ネットワークと共有センター**に進みます。
3. **接続のプロパティ**を開き、**インターネット プロトコル バージョン 4 (TCP/IPv4)** を選択し、**プロパティ**をクリックします。
4. **次のDNSサーバーのアドレスを使う**を選択し、希望のDNSサーバーのアドレスを入力します。

### Macの場合
1. **システム環境設定**を開きます。
2. **ネットワーク**を選択します。
3. 使用しているネットワーク接続を選び、**詳細**をクリックします。
4. **DNS**タブを選び、DNSサーバーのアドレスを追加または変更します。

## ステップ 4: 名前解決の確認
### コマンドプロンプトやターミナルを使って、名前解決が正しく行われているか確認します。
- Windows: `nslookup www.example.com`
- Mac/Linux: 同じく `nslookup www.example.com`

このコマンドを実行すると、ドメイン名に対応するIPアドレスが表示されるはずです。これにより、名前解決が正常に機能していることを確認できます。

## ステップ 5: トラブルシューティング
- 名前解決が機能しない場合、DNS設定を確認し、正しいアドレスが入力されているかを確認します。
- ネットワーク接続を再起動することで、一時的な問題が解決することもあります。

このガイドが、初心者の方が名前解決を理解し、実際に利用できるようになる一助となれば幸いです。名前解決は、インターネットをスムーズに利用するための基本的な技術ですので、ぜひマスターしてください。