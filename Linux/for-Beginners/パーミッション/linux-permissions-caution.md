# Linuxパーミッション - 注意点（ファイルとディレクトリ）

ファイルとディレクトリのパーミッションを扱う際は、以下の点に注意してください。

1. **ディレクトリとファイルの違いを理解する**
   - ディレクトリの実行権限（x）は、そのディレクトリへのアクセスに不可欠
   - ディレクトリの書き込み権限は、ファイルの作成・削除・名前変更に影響

2. **最小権限の原則**
   - 必要最小限のパーミッションのみを付与する
   - 特に「その他」のユーザーへの権限は慎重に設定

3. **ディレクトリのパーミッションの影響**
   - 親ディレクトリのパーミッションが子ファイル・ディレクトリへのアクセスを制限可能
   - ディレクトリに読み取り権限がなくても、実行権限があればファイルにアクセス可能

4. **再帰的変更の注意**
   - `chmod -R` の使用時は対象を慎重に選択
   - ファイルとディレクトリで異なるパーミッションが必要な場合がある

5. **特殊なパーミッションの慎重な使用**
   - SetUID、SetGID、Sticky Bitは必要な場合のみ使用
   - SetUIDはセキュリティリスクとなる可能性があるため、特に注意

6. **シンボリックリンクの扱い**
   - シンボリックリンク自体のパーミッションは意味を持たない
   - リンク先のファイル/ディレクトリのパーミッションが重要

7. **umaskの影響**
   - システムのデフォルトumask設定が新規作成ファイル/ディレクトリのパーミッションに影響

8. **ファイルシステムの制限**
   - 一部のファイルシステムではパーミッションが制限される場合がある（例：FAT32）

9. **ネットワーク共有の考慮**
   - NFS、Sambaなどでは、パーミッションの挙動が異なる可能性がある

10. **グループパーミッションの活用**
    - 適切なグループ設定と権限付与で、効率的なファイル共有が可能

11. **実行権限の慎重な付与**
    - ファイルに対する実行権限は、そのファイルが実行可能であることを確認してから付与

12. **ホームディレクトリの保護**
    - ユーザーのホームディレクトリは通常 700 (rwx------) に設定し、他のユーザーからアクセスを制限

13. **世界書き込み可能なディレクトリの危険性**
    - 777 のようなパーミッションは極力避け、特に重要なディレクトリでは使用しない

14. **定期的な監査**
    - 重要なファイル/ディレクトリのパーミッションを定期的に確認
    - 不適切なパーミッション設定を検出する自動化ツールの使用を検討

15. **パーミッションの継承**
    - 新規作成されたファイル/ディレクトリは親ディレクトリからパーミッションを継承しない
    - 必要に応じて、デフォルトACLを設定して継承をコントロール

16. **ACL（アクセス制御リスト）の考慮**
    - 標準のパーミッションだけでは不十分な場合、ACLの使用を検討

適切なファイルおよびディレクトリパーミッションの管理は、システムのセキュリティと整合性を維持する上で極めて重要です。これらの注意点を考慮し、定期的にパーミッション設定を見直すことをお勧めします。
