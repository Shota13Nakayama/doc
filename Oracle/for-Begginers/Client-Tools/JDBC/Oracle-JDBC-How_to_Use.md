# Oracle-JDBCの使い方ガイド

## はじめに
Oracle-JDBC（Java Database Connectivity）は、JavaアプリケーションからOracleデータベースに接続するための標準APIです。JDBCを使用することで、Javaプログラムからデータベース操作（クエリの実行、データの更新など）を簡単に行うことができます。

## 必要な準備
Oracle-JDBCを使用するためには、以下の準備が必要です。
1. **Oracleデータベース**：接続先となるOracleデータベースが必要です。
2. **Oracle JDBCドライバ**：Oracleから提供されるJDBCドライバ（`ojdbc.jar`）をダウンロードします。
3. **Java開発環境**：Java開発環境（JDK）がインストールされていることを確認します。

## ステップバイステップガイド

### 1. JDBCドライバの設定
まず、Oracleの公式サイトからJDBCドライバをダウンロードします。ダウンロードした`ojdbc.jar`ファイルをプロジェクトのクラスパスに追加します。

### 2. データベース接続の設定
次に、データベースに接続するための設定を行います。以下のコード例を参考にしてください。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class OracleJDBCExample {
    public static void main(String[] args) {
        // データベースのURL、ユーザー名、パスワードを指定します
        String url = "jdbc:oracle:thin:@localhost:1521:xe";
        String user = "your_username";
        String password = "your_password";

        Connection connection = null;

        try {
            // JDBCドライバをロードします
            Class.forName("oracle.jdbc.driver.OracleDriver");

            // データベースに接続します
            connection = DriverManager.getConnection(url, user, password);

            if (connection != null) {
                System.out.println("データベースに接続成功しました！");
            } else {
                System.out.println("データベースに接続できませんでした。");
            }

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 接続を閉じます
            if (connection != null) {
                try {
                    connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

### 3. クエリの実行
データベースに接続できたら、クエリを実行してデータを取得したり更新したりすることができます。以下に例を示します。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class OracleJDBCQueryExample {
    public static void main(String[] args) {
        String url = "jdbc:oracle:thin:@localhost:1521:xe";
        String user = "your_username";
        String password = "your_password";

        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            Class.forName("oracle.jdbc.driver.OracleDriver");
            connection = DriverManager.getConnection(url, user, password);

            statement = connection.createStatement();
            String query = "SELECT * FROM your_table";
            resultSet = statement.executeQuery(query);

            while (resultSet.next()) {
                System.out.println("ID: " + resultSet.getInt("id"));
                System.out.println("Name: " + resultSet.getString("name"));
            }

        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        } finally {
            if (resultSet != null) {
                try {
                    resultSet.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (statement != null) {
                try {
                    statement.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (connection != null) {
                try {
                    connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

## まとめ
以上がOracle-JDBCを使用してJavaアプリケーションからOracleデータベースに接続し、クエリを実行する基本的な手順です