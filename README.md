# MoodCinema

**MoodCinema**は、ユーザーの現在の気分に基づいて映画を推薦するウェブアプリケーションです。ユーザーは気分を自由にテキストで入力することで、その気分に合った映画を提案します。本アプリは、ChatGPTを用いた気分解析とTMDb APIを使用して映画の推薦を行います。

## 特徴

- **気分ベースの映画推薦**: 気分を入力すると、パーソナライズされた映画の提案を受け取れます。
- **インタラクティブなUI**: ReactとNext.jsを使用して、スムーズなユーザー体験を提供。
- **AIによる気分解析**: ChatGPT APIを利用してユーザーの気分を解析し、適切な映画を選定。
- **リアルタイムの映画データ**: TMDb APIを使用して最新の映画情報を取得。

## 技術スタック

- **フロントエンド**: React, Next.js
- **バックエンド**: Django
- **API**: ChatGPT API, TMDb API
- **スタイリング**: CSS
- **デプロイメント**: Vercel (フロントエンド), Azure

## インストールとセットアップ

### 前提条件

以下のソフトウェアがインストールされていることを確認してください：

- Node.js (>= 14.x)
- Python (>= 3.x)
- Django (>= 4.x)
- Virtualenv (Python仮想環境管理用)

### 1. リポジトリのクローン

```bash
git clone https://github.com/username/moodcinema.git
cd moodcinema
```

### 2. バックエンドのセットアップ (Django)

1. `backend`ディレクトリに移動し、仮想環境を作成します：

    ```bash
    cd backend
    python3 -m venv env
    source env/bin/activate
    ```

2. 必要なPythonパッケージをインストールします：

    ```bash
    pip install -r requirements.txt
    ```

3. 環境変数を設定するために、バックエンドディレクトリに`.env`ファイルを作成し、以下の内容を追加します：

    ```plaintext
    DJANGO_SECRET_KEY=your_secret_key
    CHATGPT_API_KEY=your_chatgpt_api_key
    TMDB_API_KEY=your_tmdb_api_key
    ```

4. Djangoのマイグレーションを実行します：

    ```bash
    python manage.py migrate
    ```

5. Django開発サーバーを起動します：

    ```bash
    python manage.py runserver
    ```

### 3. フロントエンドのセットアップ (Next.js)

1. `frontend`ディレクトリに移動します：

    ```bash
    cd ../frontend
    ```

2. 必要なパッケージをインストールします：

    ```bash
    npm install
    ```

3. `frontend`ディレクトリに`.env.local`ファイルを作成し、以下の内容を追加します：

    ```plaintext
    NEXT_PUBLIC_API_BASE_URL=http://localhost:8000/api
    ```

4. 開発サーバーを起動します：

    ```bash
    npm run dev
    ```

### 4. アプリケーションのテスト

バックエンド（Django）とフロントエンド（Next.js）の両方が起動したら、ブラウザで以下のURLにアクセスしてください：

```
http://localhost:3000
```

これで、気分を入力して映画の推薦を受け取ることができます！

## APIの使用方法

### ChatGPT API

バックエンドはChatGPT APIを使用して、ユーザーの自由形式の気分入力を処理します。`.env`ファイルにOpenAIのAPIキーを設定する必要があります。

- **APIエンドポイント**: `/api/analyze_mood/`
- **メソッド**: POST
- **リクエストボディ**:
  ```json
  {
    "mood_text": "落ち込んだ気持ち"
  }
  ```

### TMDb API

アプリはTMDb APIを使用して、気分に基づいた映画の推薦を取得します。

- **APIエンドポイント**: `/api/get_movies/`
- **メソッド**: GET
- **クエリパラメータ**:
  - `mood`: ChatGPT APIから返された解析済みの気分文字列。

