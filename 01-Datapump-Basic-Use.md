
# Oracle Data Pumpの使い方

## 概要

Oracle Data Pumpはデータベース間でデータを高速に移動するための強力なツールです。

主な特徴:
- エクスポート(expdp)とインポート(impdp)の2つのコマンドラインツール
- パラレル処理による高速データ転送
- メタデータのみ、データのみ、または両方の転送が可能
- フィルタリングによる部分的なエクスポート/インポート

## 主な目的
テーブルなどデータ移行やバックアップ
メタデータオンリーで情報を抜き出し、同じ状況の環境を作成する。

## 基本的な使い方

### エクスポート
```
expdp username/password DIRECTORY=data_pump_dir DUMPFILE=export.dmp
```

### インポート  
```
impdp username/password DIRECTORY=data_pump_dir DUMPFILE=export.dmp
```

## 主要なパラメータ

- FULL: 全データベースのエクスポート/インポート
- SCHEMAS: 指定したスキーマのエクスポート/インポート  
- TABLES: 指定したテーブルのエクスポート/インポート
- QUERY: データのフィルタリング
- REMAP_SCHEMA: スキーマのリマップ
- PARALLEL: 並列度の指定

## 使用例

スキーマのエクスポート:
```
expdp hr DIRECTORY=dpump_dir1 DUMPFILE=hr.dmp SCHEMAS=hr
```

テーブルのインポート:
```
impdp hr TABLES=employees,departments DUMPFILE=hr.dmp
```

## その他Tips
- パラメータファイルを使用すると長いコマンドを簡潔に記述できます
- ネットワークモードを使用するとダンプファイルなしでデータ転送が可能です
- トランスポータブルオプションを使用するとさらに高速な転送が可能です
以上が Oracle Data Pump の基本的な使い方です。状況に応じて適切なオプションを選択してください。


