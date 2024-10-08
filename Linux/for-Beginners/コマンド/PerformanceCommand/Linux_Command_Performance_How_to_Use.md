
# How to Use: Linuxパフォーマンス向上のためのコマンド

## 概要

ここでは、Linux環境でパフォーマンスを向上させるために役立つコマンドの使用方法について解説します。初心者にもわかりやすいように、各コマンドの具体的な使い方と実例を示していきます。

## CPUパフォーマンスの確認: `top` コマンド

`top`コマンドは、システム全体のCPU使用率を確認するための基本的なツールです。リアルタイムでプロセスごとのCPU使用率やメモリ使用量を監視できます。

```bash
top
```

1. コマンドを実行すると、上位のCPU使用率を持つプロセスが表示されます。
2. 必要に応じて、特定のプロセスを終了することもできます (例: `kill` コマンドを使用)。

## メモリ使用状況の確認: `free` コマンド

`free`コマンドは、メモリの使用状況を確認するためのツールです。システムの総メモリ、使用中のメモリ、空きメモリの情報が得られます。

```bash
free -h
```

- `-h`オプションを付けることで、見やすい形式で表示されます (GBやMB単位)。

## ディスクI/Oの監視: `iostat` コマンド

`iostat`コマンドは、ディスクの入出力（I/O）性能を監視するために使用されます。特にストレージのパフォーマンスに問題がある場合に役立ちます。

```bash
iostat
```

- ディスクの読み書き速度やI/O待機時間を確認できます。

## ネットワーク使用状況の確認: `ifstat` コマンド

`ifstat`コマンドは、ネットワークインターフェースごとの送受信データ量を確認できます。ネットワーク遅延や帯域幅の問題を診断する際に便利です。

```bash
ifstat
```

- 送受信データの速度をリアルタイムでモニタリングできます。

## 実行例

例えば、システム全体のパフォーマンスを確認する場合、まず`top`コマンドでCPUとメモリの使用状況を確認し、次に`iostat`でディスクI/Oの状態を確認、最後に`ifstat`でネットワークの使用状況をチェックするという手順を踏むことが一般的です。

