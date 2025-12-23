# 回答用紙 （学生用）

(本Markdownファイルを記入し、課題を完成、提出すること)

##  API実習　2025　課題レポート（第3回）

**API 実習課題**: FastAPI + Streamlit + OpenAPIドキュメントの「設計」「実装」「動作確認」

###  出題範囲：　API実習2025　第7回～第9回まで

###  提出期限：　2025/12/23(火) 17:00

-------

レポート提出者：

|クラス|学籍番号|　氏名　|
|-|-|-|
| A | 20124012 | 椛澤友悟 |


# 　**ToDo メモ管理 API 実習レポート（FastAPI / Streamlit）**

## 1. 実習の目的

（※ APIとは何か？今回の授業で学ぶことを100～200字程度で記述）
APIとは、異なるソフトウェア同士が情報をやり取りするための窓口のこと。今回の授業では、PythonのFastAPIを用いて、Streamlitでフロントエンド（画面表示）を作成することで、Webアプリケーションがどのようにデータをやり取りし、動作するのかという一連の仕組みを理解することを目的としています。
> **記入欄：**

---

## 2. API 設計（エンドポイント仕様）

| メソッド   | パス          | 内容 | リクエスト例 | レスポンス例 |
| ------ | ----------- | -- | ------ | ------ |
| GET    | /todos      |  取得  |        |    [{"id": 0, "title": "課題を出す", "done": false}] |
| POST   | /todos      |  追加  |    {"title": "買い物に行く"}    |     {"id": 1, "title": "買い物に行く", "done": false}    |
| PUT    | /todos/{id} |  更新  |        |    {"id": 1, "title": "買い物に行く", "done": true}    |
| DELETE | /todos/{id} |  削除  |        |    {"message": "Deleted"}    |

> ※ 例を JSON 形式で記載
> **記入欄：**
> 



## 3. 使用した技術構成（選択した項目に ✓）

| 使用技術            |  使用 | 備考（任意） |
| --------------- | :-: | ------ |
| FastAPI         | [✓]|        |
| Streamlit       | [✓]|        |
| SQLite（DB 永続化）  | [ ] |        |
| SQLAlchemy（ORM） | [ ] |        |
| そのほか            | [✓] |    requests, uvicorn    |

> ※ SQLite / SQLAlchemy を使用した場合は後半の加点欄も記入

---

## 4. FastAPI コード（主要部分のみ抜粋）

（※ スクリーンショット不可。**テキストで貼り付ける**）

```python
# FastAPI の主要コードをここに貼る
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from typing import List, Optional

app = FastAPI()

class Todo(BaseModel):
    id: Optional[int] = None
    title: str
    done: bool = False

todos = []
id_counter = 0

@app.get("/todos", response_model=List[Todo])
def get_todos():
    return todos

@app.post("/todos", response_model=Todo)
def create_todo(todo: Todo):
    global id_counter
    todo.id = id_counter
    todos.append(todo)
    id_counter += 1
    return todo

@app.put("/todos/{todo_id}")
def update_todo(todo_id: int):
    for todo in todos:
        if todo.id == todo_id:
            todo.done = not todo.done 
            return todo
    raise HTTPException(status_code=404, detail="Todo not found")

@app.delete("/todos/{todo_id}")
def delete_todo(todo_id: int):
    for index, todo in enumerate(todos):
        if todo.id == todo_id:
            todos.pop(index)
            return {"message": "Deleted"}
    raise HTTPException(status_code=404, detail="Todo not found")
```

---

## 5. OpenAPI ドキュメント動作確認（スクリーンショット貼付）

| 操作         | 貼付欄 |
| ---------- | --- |
| POST（新規追加） |  <img width="1831" height="654" alt="image" src="https://github.com/user-attachments/assets/a3ba31cc-18e7-43fc-8492-ad0e908ab72c" />
<img width="1830" height="697" alt="image" src="https://github.com/user-attachments/assets/ad5c0d6d-7cc6-4b4b-a8e9-2c02601886c6" /><img width="1831" height="471" alt="image" src="https://github.com/user-attachments/assets/ca7636d8-4fcf-4736-bcd3-c81fbb428e7f" />

|
| GET（一覧取得）  |  <img width="1827" height="819" alt="image" src="https://github.com/user-attachments/assets/4076b91b-3280-427e-b119-8e1fd2875ae1" />
<img width="1826" height="713" alt="image" src="https://github.com/user-attachments/assets/6620a5cb-0986-49ce-a3d1-d7619687586b" />
|
| PUT（更新）    |  <img width="1827" height="790" alt="image" src="https://github.com/user-attachments/assets/01a670f0-ff2d-4b3e-83a5-c805f34f17bf" />
<img width="1832" height="602" alt="image" src="https://github.com/user-attachments/assets/9427d41f-9e3a-4dfd-b36c-1265807c1453" />
 |
| DELETE（削除） |  <img width="1829" height="801" alt="image" src="https://github.com/user-attachments/assets/86d2f9dd-35c6-4ade-8807-6a492a0d6585" />
<img width="1829" height="562" alt="image" src="https://github.com/user-attachments/assets/f4cf27e1-35e6-4861-8649-46a357abf039" />
|


---

## 6. Streamlit 画面 UI（スクリーンショット貼付）

| 画面キャプチャ       | 貼付欄 |
| ------------- | --- |
| 実行画面          |   <img width="1270" height="605" alt="image" src="https://github.com/user-attachments/assets/96f30a4f-abd3-49d1-b9d6-f332bc3ef615" />

  |
| 操作例（追加・更新・削除） |  <img width="1168" height="668" alt="image" src="https://github.com/user-attachments/assets/ad2ca5e4-6ac2-460c-8fc3-10758b501cd2" />
  |

---

## 7. API 通信ログ（サーバログ or Web通信キャプチャなど）

サーバーコンソールやログ画面のキャプチャを 1 枚以上添付

| ログ例（貼付欄） |
| -------- |
|      <img width="1146" height="770" alt="スクリーンショット 2025-12-18 212305" src="https://github.com/user-attachments/assets/9d8f4916-fa85-4449-be5e-af46d65d7a28" />
   <img width="1163" height="806" alt="スクリーンショット 2025-12-18 212326" src="https://github.com/user-attachments/assets/ab44dcc1-5438-4209-88ce-d63b3ba7c7f0" />
 |

---

## 8. 学習したこと・感想（100文字以上）

> **記入欄：**
FastAPIを使うことで、コードを書くだけで自動的にOpenAPIという仕様書が生成され、ブラウザから簡単に動作確認ができる点に驚きました。また、Streamlitとrequestsライブラリを組み合わせることで、複雑なHTML/CSSを書かなくても実用的なWebサイトが作れることを学びました。フロントエンドとバックエンドを分けて開発し、それらをHTTP通信でつなぐというモダンな開発手法の基礎を体験できて非常に有益でした。

## チャレンジ課題：  9. SQLite / SQLAlchemy 導入内容

（使用した人のみ記述）

### 9-1. ER図（例：テーブル）

```
# 具体例を書いたり、手書きを撮影して貼っても良い

```

### 9-2. DB を使うメリット

> **記入欄：**

### 9-3. SQLAlchemy を使用した理由

> **記入欄：**


## 10. 参考資料（使用した場合のみ記入）

| 種類     | URL / 書籍名 |
| ------ | --------- |
| Webサイト |      ・https://qiita.com/Hashimoto-Noriaki/items/6dbefe8068dbfe2c236d  ・https://www.aeyescan.jp/blog/openapi/　・https://zenn.dev/upgradetech/articles/8d81f8a8df88cc　・https://zenn.dev/homatsu_tech/articles/d664a65b776efe  |
| 書籍     |           |
| その他    |           |

**提出前チェックリスト**

* ✓ API のコードを貼った
* ✓ OpenAPI のスクリーンショットを貼った
* ✓ Streamlit UI の画像を貼った
* ✓ 学習したことを 100 字以上書いた
* [ ] SQLite / SQLAlchemy の加点欄（使った場合のみ）






