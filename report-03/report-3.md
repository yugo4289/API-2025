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
| そのほか            | [✓] |        |

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
| POST（新規追加） |   <img width="1826" height="699" alt="スクリーンショット 2025-12-18 201341" src="https://github.com/user-attachments/assets/a1b51a4d-b2e0-4b85-978a-35eae9e0c2ca" /><img width="1840" height="522" alt="image" src="https://github.com/user-attachments/assets/3c4a5d8b-3e96-4b39-99a9-f04f5e2bbe38" />|
| GET（一覧取得）  |  <img width="1823" height="824" alt="image" src="https://github.com/user-attachments/assets/aca20d36-9f70-4064-ab45-9790a308d824" /><img width="1818" height="827" alt="image" src="https://github.com/user-attachments/assets/a571d245-ef66-428e-988a-1556e8269217" />|
| PUT（更新）    |  <img width="1823" height="825" alt="image" src="https://github.com/user-attachments/assets/095178f2-d92f-4797-8349-05222cb99633" /><img width="1823" height="716" alt="image" src="https://github.com/user-attachments/assets/f84f0b55-5439-4a49-bf3d-8dc0c9bfd786" /> |
| DELETE（削除） |   <img width="1830" height="822" alt="image" src="https://github.com/user-attachments/assets/1fffbcf9-74e0-4bdf-b58b-00422a9e2ad0" /><img width="1833" height="702" alt="image" src="https://github.com/user-attachments/assets/6f1138a7-7bfa-401a-8e60-0cb9b46040c2" />|


---

## 6. Streamlit 画面 UI（スクリーンショット貼付）

| 画面キャプチャ       | 貼付欄 |
| ------------- | --- |
| 実行画面          |   <img width="1147" height="503" alt="image" src="https://github.com/user-attachments/assets/e91492ed-d0ce-4682-be4e-3dd243ba826b" />
  |
| 操作例（追加・更新・削除） |  <img width="1182" height="632" alt="image" src="https://github.com/user-attachments/assets/27a6a6d7-1dbe-4aa0-b01b-d5e2de22007d" />   |

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
| Webサイト |      ・https://qiita.com/Hashimoto-Noriaki/items/6dbefe8068dbfe2c236d  ・https://zenn.dev/upgradetech/articles/8d81f8a8df88cc　　・https://zenn.dev/homatsu_tech/articles/d664a65b776efe  |
| 書籍     |           |
| その他    |           |

**提出前チェックリスト**

* [] API のコードを貼った
* [ ] OpenAPI のスクリーンショットを貼った
* [ ] Streamlit UI の画像を貼った
* [ ] 学習したことを 100 字以上書いた
* [ ] SQLite / SQLAlchemy の加点欄（使った場合のみ）


