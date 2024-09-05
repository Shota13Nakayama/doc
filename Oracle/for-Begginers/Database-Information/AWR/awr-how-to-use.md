# How to Use AWR

AWRを効果的に使用するための基本的な手順を説明します。

## 1. AWRスナップショットの確認

まず、現在のAWRスナップショットの設定を確認します。

```sql
SELECT snap_interval, retention FROM dba_hist_wr_control;
```

この結果から、スナップショットの間隔や保持期間を確認できます。

## 2. AWRレポートの生成

AWRレポートを生成するには、通常以下の2つの方法があります：

### a. SQL*Plusを使用する方法

1. SQL*Plusに接続します。
2. 以下のスクリプトを実行します：

実行可能なスクリプトは多種あります。
RACなのかSingleデータベースなのかなどご注意ください
https://princetonits.com/blog/technology/oracle-awr-ash-and-addm-reports-for-rac/

```sql
@$ORACLE_HOME/rdbms/admin/awrrpt.sql
```

3. プロンプトに従って、レポートの形式（HTML or TEXT）、開始と終了のスナップショットID、レポートの名前を入力します。

### b. Enterprise Managerを使用する方法

1. Enterprise Managerにログインします。
2. 対象のデータベースを選択します。
3. パフォーマンス → AWRレポート を選択します。
4. レポートのオプションを選択し、生成 をクリックします。

## 3. AWRレポートの分析

生成されたAWRレポートには多くの情報が含まれています。以下は重要なセクションです：

1. **Report Summary**: レポートの概要と基本情報
2. **Time Model Statistics**: データベース時間の内訳
3. **Operating System Statistics**: OSレベルの統計情報
4. **Wait Events Statistics**: 待機イベントの統計
5. **SQL Statistics**: 実行時間やI/Oが多いSQLの一覧

## 分析の具体例

例えば、データベースの応答が遅いという問題が発生した場合：

<実行SQL確認>
1. 問題発生前後のAWRレポートを生成
2. "SQL ordered by Elapsed Time"セクションを確認し、特に長い実行時間のSQLを特定
3. ExecutionやElapsed Time per Execも確認し、遅延原因を特定
4. 必要に応じSQLレポートやDBMS_XPLAN.DISPLAY_AWRなどから実行計画を確認


<待機イベント確認>
1. 問題発生前後のAWRレポートを生成
2. "Top 5 Timed Events" セクションを確認し、主な待機要因を特定
3. もし "db file sequential read" が上位にある場合、インデックスの追加や再構築を検討
4. "SQL ordered by Elapsed Time" セクションで、実行時間の長いSQLを確認し、チューニングを検討

<インスタンス効率の確認>

1. "Instance Efficiency Percentages" セクションを確認
2. Buffer Nowait %、Redo Nowait %、SQL Service Response Timeなどの指標を確認
3. これらの値が低下している場合、それぞれバッファキャッシュ、REDOログバッファ、SQLパフォーマンスに問題がある可能性を検討

<I/Oパフォーマンスの確認>

1. "IO Profile" セクションを確認
2. 読み取り/書き込みの比率、平均I/O時間などを確認
3. I/O時間が長い場合、ストレージシステムの問題や不適切なI/O分散を疑う

<リソース使用状況の確認>

1. "Operating System Statistics" セクションを確認
2. CPU使用率、メモリ使用量、ディスクI/O統計を確認
3. 前回のAWRレポートと比較し、急激な変化がないか確認
4. 例えば、CPU使用率が90%を超えている場合、CPUバウンドな問題の可能性を検討

<SQL統計の詳細分析>

1. "SQL Statistics" セクションの "SQL ordered by Parse Calls" を確認
2. 頻繁にパースされているSQLを特定し、バインド変数の使用を検討
3. "SQL ordered by Version Count" で、バージョン数の多いSQLを確認し、SQLの再利用性を向上させる方法を検討

<ADDMによる推奨事項を確認>
1. 問題発生前後のAWRレポートを生成
2. 問題発生後のAWRレポート内でADDMによる自動問題診断・解決策掲示がされていないかを確認。


<セグメント統計の確認>

1. "Segments by Physical Reads" や "Segments by Row Lock Waits" などのセクションを確認
2. 特定のテーブルやインデックスに負荷が集中していないか確認
3. 必要に応じて、パーティショニングやインデックス再構築を検討

<ラッチ競合の確認>

1. "Latch Statistics" セクションを確認
2. 特に高い待機時間を示すラッチがないか確認
3. 例えば、"cache buffers chains" ラッチの競合が高い場合、バッファキャッシュのサイズ調整を検討

このように、AWRレポートを活用することで、効果的にパフォーマンス問題を特定し、解決策を見出すことができます。
