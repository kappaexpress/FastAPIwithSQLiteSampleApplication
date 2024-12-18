# 開始手順
1.  **GitHubリポジトリを開く:**
    *   まず、ブラウザでGitHubにアクセスし、対象のリポジトリを開きます。

2.  **「Code」ボタンをクリック:**
    *   リポジトリページの上部にある緑色の「Code」ボタンをクリックします。

3.  **「Codespaces」タブを選択:**
    *   ポップアップメニューが表示されるので、「Codespaces」タブをクリックします。

4.  **「Create codespace on main」をクリック:**
    *   「No codespaces」という表示が出ている場合は、「Create codespace on main」と書かれた緑色のボタンをクリックします。これにより、リポジトリのメインブランチを基にした新しいCodespaceが作成されます。
    *   この処理には少し時間がかかります。画面が切り替わるまでお待ちください。
    *   すでにCodespaceが作成されている場合は、そのまま次の手順に進みます。

5.  **VS Codeが起動:**
    *   Codespaceの作成が完了すると、Webブラウザ上でVisual Studio Code（VS Code）が起動します。
    *   初期起動時には、いくつかのメッセージが表示される場合があります。

6.  **ファイルを開く:**
    *   VS Codeの左側にあるエクスプローラー（ファイル一覧）から、目的のファイルを開いて内容を確認できます。
        *   例：`README.md`をクリックすると、リポジトリの説明が表示されます。
        *   例：`client.html`をクリックすると、HTMLファイル（フロントエンド）の内容が表示されます。
        *   例：`server.py`をクリックすると、Pythonファイル（バックエンド）の内容が表示されます。

7.  **アプリケーションサーバーの起動:**
    *   ターミナルを開いて、以下のコマンドを入力してアプリケーションサーバーを起動します。
    *  初回実行時に、ブラウザにクリップボードへのアクセス許可を求められる場合があります。「許可する」をクリックします。
    ```bash
    uvicorn server:app --host 0.0.0.0 --port 8000 --reload
    ```

8.  **Live Serverを起動:**
    *  VS Codeの右下にある「Go Live」をクリックします。

9.  **ブラウザでHTMLを開く:**
    *  Live Serverの起動後、Webブラウザにアプリケーションが表示されます。
    *  client.htmlを開いて、アプリケーションの動作を確認できます。
    *  初回設定前は、エラーのポップアップがでます

10.  **コードの編集:**
    *  VS Code上でファイルを編集し、保存する.
    *  例：`client.html`を開いて、HTMLコードを変更して保存すると、ブラウザが自動でリロードされます。
    *  例：`server.py`を開いて、Pythonコードを変更して保存すると、サーバーが再起動されます。

11.  **初回の設定変更**
    *  初回設定時には、APIサーバーのホスト名を変更する必要があります。

    *  `client.html`ファイルを開いて、以下のコードを変更します。(34行目付近)

    *  変更前のコード
    ```javascript
    // APIサーバーのベースURL（それぞれで違います）
    const API_URL = "http://localhost:8000/todos"
    ```

    変更後のコード
    ```javascript
    // APIサーバーのベースURL（それぞれで違います）
    const API_URL = "https://saisyonikakikaeru-8000.app.github.dev/todos"
    ```


**用語解説:**

*   **GitHub Codespaces:** Webブラウザ上で開発環境を構築・利用できる機能です。
*   **VS Code (Visual Studio Code):** Microsoftが開発した無料のコードエディターです。
*   **リポジトリ:** プロジェクトのソースコードや関連ファイルを保存する場所です。
*   **ブランチ:** リポジトリ内の異なるバージョンや開発ラインを管理するための仕組みです。
*   **Live Server:** VS Codeの拡張機能で、HTMLファイルなどを変更すると、ブラウザに自動で反映させることができます。
*   **ターミナル:** コンピュータへのコマンドを入力するためのインターフェースです。
*   **ポート:** インターネットを介して通信するために使用される、コンピュータ上の番号です。

# 考え方

1. **要件定義**
   - まず作りたいアプリケーションの目的を明確にする
   - どんなデータを扱いたいか考える（例：TODO管理→レシピ管理、メモ帳、家計簿など）
   - どんな機能が必要か洗い出す（基本的なCRUD操作に加えて必要な機能）

2. **データモデルの設計**
   - 保存したいデータの構造を決める
   - テーブル設計（必要なカラムとその型を決める）
   - サンプルコードのTodoクラスを参考に、自分のデータモデルを定義

3. **基本的なCRUD操作の実装**
   - サンプルコードを参考に、以下の基本機能を実装：
     - Create（データの作成）
     - Read（データの読み取り）
     - Update（データの更新）
     - Delete（データの削除）

4. **追加機能の実装(余裕あれば)**
   - 基本機能ができたら、オリジナルの機能を追加
   - 例えば：
     - 検索機能
     - データのフィルタリング
     - ソート機能
     - カテゴリ分け

5. **エラーハンドリングの追加(余裕あれば)**
   - ユーザーの入力チェック
   - エラーメッセージの改善
   - 例外処理の追加

具体例として、簡単なレシピ管理アプリケーションを作る場合の流れを見てみましょう：

1. **要件定義の例**
レシピ管理アプリケーション
- レシピの登録、表示、更新、削除ができる
- レシピには料理名、材料、手順、調理時間を登録できる
- カテゴリ（和食、洋食など）で分類できる
- 調理時間で検索できる

2. **データモデルの設計例**
```python
from pydantic import BaseModel
from typing import List, Optional

class Recipe(BaseModel):
    title: str
    ingredients: List[str]
    steps: List[str]
    cooking_time: int  # 分単位
    category: str
```

3. **データベース設計例**
```python
def init_db():
    with sqlite3.connect('recipes.db') as conn:
        conn.execute('''
            CREATE TABLE IF NOT EXISTS recipes (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                title TEXT NOT NULL,
                ingredients TEXT NOT NULL,  # JSON形式で保存
                steps TEXT NOT NULL,        # JSON形式で保存
                cooking_time INTEGER NOT NULL,
                category TEXT NOT NULL
            )
        ''')
```

4. **基本的なエンドポイントの実装例**
```python
# レシピの新規作成
@app.post("/recipes", response_model=RecipeResponse)
def create_recipe(recipe: Recipe):
    # 実装内容

# レシピの検索（調理時間でフィルタリング）
@app.get("/recipes/search")
def search_recipes(max_time: Optional[int] = None):
    # 実装内容
```

段階的に機能を追加していくことで、複雑なアプリケーションも整理して実装することができます。

アドバイス：
1. まずは小さな機能から始める
2. 動作確認を細かく行う
3. 機能を少しずつ追加する
4. エラーが出たら、エラーメッセージをよく読んで対処する
5. コードにコメントを書いて、後で見返したときに理解できるようにする

# 役に立つコマンド
## ライブラリのインストール
```bash
pip install -r requirements.txt
```

## サーバーを起動するコマンド
```bash
uvicorn server:app --host 0.0.0.0 --port 8000 --reload
```