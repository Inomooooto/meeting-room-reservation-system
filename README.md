# 会議室予約システム

## プロジェクト概要

職業訓練校でのチーム開発プロジェクトとして作成した、会議室予約管理システムです。
Java Servlet + JSP を使用したWebアプリケーションで、会議室の予約・管理を効率的に行うことができます。

## 主な機能

- **ユーザー認証**
  - ログイン/ログアウト機能
  - セッション管理

- **会議室管理**
  - 会議室の登録・削除
  - 会議室情報の表示

- **予約管理**
  - 会議室の予約登録
  - 予約の取り消し
  - 予約状況の確認

- **ユーザー管理**
  - ユーザーの作成・更新・削除
  - ユーザー情報の検索

## 技術スタック

### バックエンド
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Servlet](https://img.shields.io/badge/Servlet-3.0+-007396?style=flat-square)
![JSP](https://img.shields.io/badge/JSP-JavaServer_Pages-007396?style=flat-square)
![JDBC](https://img.shields.io/badge/JDBC-Database_Connectivity-007396?style=flat-square)

- Java SE 8
- Java Servlet 3.0+
- JSP (JavaServer Pages)
- JDBC (Java Database Connectivity)

### データベース
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)

- PostgreSQL / MySQL
- SQL（DDL/DML）

### フロントエンド
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)

- HTML5
- CSS3
- JavaScript

### インフラ・ツール
![Apache Tomcat](https://img.shields.io/badge/Apache_Tomcat-F8DC75?style=flat-square&logo=apachetomcat&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=flat-square&logo=apachemaven&logoColor=white)

- Apache Tomcat 9.x
- Git / GitHub
- Maven / Gradle（ビルドツール）

### 開発手法
- MVCパターン
- レイヤードアーキテクチャ
- チーム開発（Git Flow）

## プロジェクト構成

```
java-meetingroom/
├── DB/                         # データベース関連
│   ├── database.sql            # テーブル定義
│   └── testdata.sql            # テストデータ
└── src/main/
    ├── java/jp/co/seminar/
    │   ├── bean/               # データモデル (Bean)
    │   ├── dao/                # データアクセス層 (DAO)
    │   ├── filter/             # 共通フィルター処理
    │   ├── servlet/            # コントローラー (Servlet)
    │   │   ├── main/           # メイン機能
    │   │   ├── meetingRoom/    # 会議室管理
    │   │   ├── reservation/    # 予約管理
    │   │   └── user/           # ユーザー管理
    │   └── util/               # ユーティリティ (DB接続等)
    └── webapp/
        ├── css/                # スタイルシート
        └── jsp/                # ビュー (JSP)
            ├── login.jsp       # ログイン画面
            ├── menu.jsp        # メニュー画面
            ├── cancel/         # 予約取消画面
            ├── meetingRoom/    # 会議室管理画面
            ├── reservation/    # 予約登録画面
            └── userSituation/  # ユーザー管理画面
```

## セットアップ方法

### 1. データベースのセットアップ

```bash
# データベースの作成
psql -U postgres -c "CREATE DATABASE meeting_room;"

# テーブルの作成
psql -U postgres -d meeting_room -f DB/database.sql

# テストデータの投入
psql -U postgres -d meeting_room -f DB/testdata.sql
```

### 2. データベース接続設定

`src/main/java/jp/co/seminar/util/DatabaseConfig.java` でデータベース接続情報を設定してください。

### 3. アプリケーションのビルドと起動

```bash
# ビルド (Mavenの場合)
mvn clean package

# Tomcatにデプロイ
# 生成された war ファイルを Tomcat の webapps ディレクトリに配置

# Tomcat起動
catalina.sh run
```

### 4. アクセス

ブラウザで以下のURLにアクセス：
```
http://localhost:8080/meetingroom/
```

## 開発のポイント

### アーキテクチャ

- **MVCパターン**の採用
  - Model: Bean + DAO
  - View: JSP
  - Controller: Servlet

- **レイヤードアーキテクチャ**
  - プレゼンテーション層（JSP）
  - ビジネスロジック層（Servlet）
  - データアクセス層（DAO）

### セキュリティ対策

- セッション管理によるログイン状態の保持
- フィルターによる未認証アクセスの制御
- エンコーディングフィルターによる文字化け対策
- SQLインジェクション対策（PreparedStatement使用）

### エラーハンドリング

- カスタム例外クラス（AppException）の実装
- エラー画面への適切な遷移

## 開発体制

- **チーム構成**: 6名
- **開発期間**: 約2週間（2025年1月）
- **開発手法**: アジャイル開発、Git Flow

## 担当と役割

### ポジション: テックリーダー

**技術面の責任範囲**
- アーキテクチャ設計とMVCパターンの実装方針策定
- コーディング規約の策定とコードレビュー
- Git運用ルールの策定とブランチ戦略の管理
- チームメンバーの技術サポートとペアプログラミング

**開発担当**
- **サービスクラス（ビジネスロジック層）の設計・実装**
  - 予約管理、会議室管理、ユーザー管理の複雑なビジネスロジック実装
  - バリデーション処理とトランザクション制御
  - Servlet から DAO への橋渡しとなる中間層の構築
- 会議室管理機能の設計・実装（Servlet、DAO、JSP）
- 共通フィルター処理の実装（認証、エンコーディング、セッション管理）
- 全体のCSS設計とレイアウト実装
- カスタム例外処理の設計と実装

**主な実装コンポーネント**
- `jp.co.seminar.service.*` - サービス層（ビジネスロジック）
- `jp.co.seminar.servlet.meetingRoom.*` - 会議室管理Servlet
- `jp.co.seminar.filter.*` - 共通フィルター
- `jp.co.seminar.bean.AppException` - 例外処理クラス
- `webapp/css/style.css` - CSSデザイン全体

## 今後の改善案

- フロントエンドフレームワーク（React/Vue.js）の導入
- RESTful API化
- Spring Boot への移行
- ユニットテストの追加（JUnit、Mockito）
- レスポンシブデザイン対応
- 予約の重複チェック機能の強化
- Docker化による環境構築の簡素化

## ライセンス

このプロジェクトは学習目的で作成されたものです。

---

**Note**: このプロジェクトは職業訓練校でのチーム開発課題として作成されました。
