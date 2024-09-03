# systemd: 使用方法

systemdを使用してLinuxシステムとサービスを管理する基本的な方法を以下に示します：

1. **サービスの管理**:
   - 起動: `sudo systemctl start service_name.service`
   - 停止: `sudo systemctl stop service_name.service`
   - 再起動: `sudo systemctl restart service_name.service`
   - 状態確認: `systemctl status service_name.service`

2. **システム起動時の自動起動設定**:
   - 有効化: `sudo systemctl enable service_name.service`
   - 無効化: `sudo systemctl disable service_name.service`

3. **システムの状態管理**:
   - 再起動: `sudo systemctl reboot`
   - シャットダウン: `sudo systemctl poweroff`

4. **ユニットファイルの管理**:
   - ユニットファイルの確認: `systemctl cat service_name.service`
   - ユニットファイルの編集: `sudo systemctl edit service_name.service`
   - 変更の反映: `sudo systemctl daemon-reload`

5. **ログの確認**:
   - システムログの表示: `journalctl`
   - 特定サービスのログ表示: `journalctl -u service_name.service`

6. **ブート時間の分析**:
   - `systemd-analyze`
   - 詳細な分析: `systemd-analyze blame`

7. **システムターゲットの管理**:
   - 現在のターゲット確認: `systemctl get-default`
   - ターゲットの変更: `sudo systemctl set-default target_name.target`

8. **依存関係の確認**:
   - `systemctl list-dependencies service_name.service`

9. **カスタムサービスの作成**:
   カスタムサービスを作成するには、以下の手順に従います：

   a. サービスユニットファイルの作成:
      `/etc/systemd/system/` ディレクトリに `.service` 拡張子のファイルを作成します。

   b. サービスユニットファイルの編集:
      必要な設定を記述します。基本的な構造は以下の通りです：

      ```
      [Unit]
      Description=サービスの説明

      [Service]
      ExecStart=実行するコマンド
      Restart=always
      User=実行ユーザー

      [Install]
      WantedBy=multi-user.target
      ```

   c. システムの再読み込みと有効化:
      ```
      sudo systemctl daemon-reload
      sudo systemctl enable your_service_name.service
      sudo systemctl start your_service_name.service
      ```

   **例1: JMeterスレーブサーバのサービス化**

   `/etc/systemd/system/jmeter-slave.service` ファイルを作成し、以下の内容を記述します：

   ```
   [Unit]
   Description=JMeter Slave Server
   After=network.target

   [Service]
   ExecStart=/path/to/jmeter/bin/jmeter-server
   Restart=always
   User=jmeter
   Environment=JMETER_HOME=/path/to/jmeter

   [Install]
   WantedBy=multi-user.target
   ```

   **例2: シェルスクリプトのサービス化**

   まず、シェルスクリプト（例：`/home/user/myscript.sh`）を作成します：

   ```bash
   #!/bin/bash
   while true; do
       echo "Running my script" >> /tmp/myscript.log
       sleep 60
   done
   ```

   次に、`/etc/systemd/system/myscript.service` ファイルを作成し、以下の内容を記述します：

   ```
   [Unit]
   Description=My Custom Script Service
   After=network.target

   [Service]
   ExecStart=/bin/bash /home/user/myscript.sh
   Restart=always
   User=user

   [Install]
   WantedBy=multi-user.target
   ```

   両方の例で、サービスを有効化し起動するには以下のコマンドを使用します：

   ```
   sudo systemctl daemon-reload
   sudo systemctl enable jmeter-slave.service  # または myscript.service
   sudo systemctl start jmeter-slave.service   # または myscript.service
   ```

これらのコマンドとカスタムサービスの作成方法を使用することで、systemdを通じてLinuxシステムとサービスを効果的に管理できます。必要に応じて `man systemctl` や `man journalctl` でさらに詳細な情報を確認できます。
