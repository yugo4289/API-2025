##  API実習　2025　課題レポート（第1回）修正版

####  ドラフト修正箇所
*  SheetDB無償APIの範囲内で、PATCH操作（部分更新）に修正、動作確認
*  REST4原則のチェックリストを教材テキストと整合


###  出題範囲：　API実習2025　第1回～第3回まで

###  提出期限：　2025/12/2(火) 17:00

###  提出方法：

- Githubアカウントの作成
- Githubアカウントの通知：FORMSで回答する：　**https://forms.office.com/r/CL1s98xPes**
- プライベートリポジトリの作成
- プライベートリポジトリへ、``keythrive`` を招待し承諾を得る
- **11/30までにここまで実施**する
- 課題に取り組む： Python環境**Colaboratory, Jupyter，VSCode**などで**コード記述**し，**必ず実行動作確認**する
- 課題の回答，レポートは，本マークダウンファイル（WebClassからダウンロード）を書き換えて，**自分の言葉で記述すること**
- ファイル名はそのままでよい。提出者はアカウントで特定可能
- **生成AIの回答，他学生のレポート内容をコピー＆ペーストしてはいけません**（明らかに不正行為で，自分の成長を妨げる弊害です）
- わからない問題は，進んでいる友達，学習支援センター，教員に質問して，必ず自分の理解とスキルにつなぐこと
- **考え方や不明な点を生成AIに質問して、回答そのものをもらうのではなく、考え方のヒントを聞いて、しっかり自分の中に消化吸収することは許容範囲内**
- 
- 各自のGithubのプライベートリポジトリ: https://github.com/アカウント/API-2025/report-01/ に、作成した課題レポートファイル一式をアップロード(push)、**必ずコミット**する
- 提出期限まで、ファイルの差し替え・アップデートは自由に可能
- 提出期限を過ぎたら、教員が自動取得する（**〆切を過ぎたら、差し替えできません**）

#####  指導教員：　情報学部　堀川

-------

レポート提出者：

|クラス|学籍番号|　氏名　|
|-|-|-|
|A| 20124012 | 椛澤友悟 |


------

## 目次

## **SheetDB CRUD演習用課題レポート（11項目）**

GoogleスプレッドシートをAPI化し、SheetDBでCRUD操作を学ぶための演習課題

***

### **課題テーマ：Googleスプレッドシートをデータベースとして扱うAPI演習**

#### **前提条件**

*   Googleスプレッドシートを作成（1行目にカラム名：`id`, `name`, `email`, `score`）
*   **適当にダミーの成績データを登録する（実際の個人情報は使わない）**
*   SheetDBでAPIを作成し、エンドポイントを取得（例：`https://sheetdb.io/api/v1/XXXXXX`）
*   PostmanまたはcURLでAPIを操作して動作確認、期待した動きかどうか説明
*   更新系は、SheetDBスプレッドシート本体にデータが追加されたことを確認
*   動作確認の証跡としてスクリーンキャプチャを貼付


####  ドラフト修正箇所

*  PUT（完全更新）と PATCH（部分更新）は有償プランが必要なため、この課題から除外
  

***

### **課題一覧（10項目）**

1.  **APIエンドポイント確認**
    *   SheetDBで作成したAPIのURLを確認し、ブラウザでアクセスしてJSONレスポンスを表示

<img width="1724" height="706" alt="スクリーンショット 2025-11-25 115557" src="https://github.com/user-attachments/assets/548e3d14-253c-454a-8458-cfa188326f6c" />

2.  **READ操作（GET）**
    *   全データを取得するGETリクエストをPostmanで送信。
    *   クエリパラメータ `limit` と `offset` を使ってページネーションの動作確認を実施

<img width="1691" height="817" alt="スクリーンショット 2025-11-25 115527" src="https://github.com/user-attachments/assets/6658673d-d64e-49d5-ba96-eb0bbd6bc9e3" />

<img width="1724" height="706" alt="スクリーンショット 2025-11-25 115557" src="https://github.com/user-attachments/assets/548e3d14-253c-454a-8458-cfa188326f6c" />

3.  **条件検索（GET with Query）**
    *   `name` が「田中」のレコードだけ取得するGETリクエストを実行

<img width="1681" height="797" alt="スクリーンショット 2025-11-25 115438" src="https://github.com/user-attachments/assets/31df806f-cc72-4c5c-833a-50fa12728019" />

4.  **CREATE操作（POST）**
    *   新しいレコード（例：`id=101, name=田中, email=test@example.com, score=85`）を追加

<img width="978" height="555" alt="スクリーンショット 2025-11-25 103808" src="https://github.com/user-attachments/assets/ff26bc57-8974-49e1-93bd-f09427ee6a85" />

<img width="939" height="401" alt="スクリーンショット 2025-11-25 120245" src="https://github.com/user-attachments/assets/42533576-17c7-42ad-a9e5-e41cd131c70d" />

5.  **複数レコード追加（POST）**
    *   `data` 配列で複数レコードを一度に追加する。

<img width="939" height="401" alt="スクリーンショット 2025-11-25 120245" src="https://github.com/user-attachments/assets/a8385913-0e7f-420f-ad3a-f5058b0dd75f" />

<img width="921" height="317" alt="スクリーンショット 2025-11-25 154655" src="https://github.com/user-attachments/assets/b8e2a7ca-98c1-4976-ad02-b3071e187aaf" />

6.  **DELETE操作**
    *   `id=101` のレコードを削除するDELETEリクエストを送信

<img width="1263" height="652" alt="スクリーンショット 2025-11-26 000650" src="https://github.com/user-attachments/assets/2fbd878a-ff65-4606-888e-68653a4d9717" />

<img width="825" height="310" alt="スクリーンショット 2025-11-26 000842" src="https://github.com/user-attachments/assets/2bbce39e-354f-474a-8fc2-c2d9e2a5d037" />

7.  **認証設定**
    *   SheetDBの管理画面でBasic認証を設定し、Postmanで認証付きリクエストを送信
  
<img width="1414" height="248" alt="スクリーンショット 2025-12-01 102042" src="https://github.com/user-attachments/assets/4ad99a99-249d-4972-b6e7-9641b7d85c54" />

<img width="1683" height="671" alt="スクリーンショット 2025-11-26 134010" src="https://github.com/user-attachments/assets/bbe3524c-dad1-4a39-9578-813a6f9c6c8f" />


8. **エラーハンドリング**
    *   存在しない `id` を指定してDELETEを実行し、レスポンスのエラー内容を確認

<img width="1691" height="733" alt="スクリーンショット 2025-12-01 103154" src="https://github.com/user-attachments/assets/08d1d920-7228-466f-9fd6-54fdf21b197b" />


9. **PATCH操作（部分更新）** **修正課題**
    SheetDB無償API利用範囲で、適切なPATCH操作を行い、特定のデータを部分更新し、レスポンスを確認する：
    * エンドポイント：　https://sheetdb.io/api/v1/XXXXXX/id/23`
    * ヘッダ：　Content-Type: application/json
    * ボディ(raw json) ：
     { 
        "email": "foo@bar.baz",
    }
    * レスポンス：　HTTPステイタスコード：　200 OK
　　* curlコマンドでの動作確認も可能

<img width="1655" height="455" alt="スクリーンショット 2025-12-01 103834" src="https://github.com/user-attachments/assets/d66eafcc-c732-4974-8ae4-e2e9081a0863" />

<img width="658" height="250" alt="スクリーンショット 2025-12-01 103616" src="https://github.com/user-attachments/assets/12ded38e-6893-4415-aa62-f5e8f0bd3f6e" />

10. **RESTの4原則対応表**
    * 上記9の設問について、下記の4原則のどれを満たしているかを表にまとめよ：

**対応表**
|番号|アドレス可能性|統一インターフェース|ステートレス|接続性|
|-|-|-|-|-|
|1|満たす|満たす|満たす|満たさない|
|2|満たす|満たす|満たす|満たさない|
|3|満たす|満たす|満たす|満たさない|
|4|満たさない|満たす|満たす|満たさない|
|5|満たさない|満たす|満たす|満たさない|
|6|満たす|満たす|満たす|満たさない|
|7|満たす|満たす|満たす|満たさない|
|8|満たす|満たす|満たす|満たさない|
|9|満たす|満たす|満たす|満たさない|



###### RESTの4原則

1.	アドレス可能性： 情報リソースはURIで一意に特定、規則的に参照
2.	統一インターフェース → HTTPメソッド（Post/Get/Put/Delete）でリソースを操作 
3.	ステートレス → 各リクエストは独立し、サーバは状態をもたない、状態管理しない
4.	接続性：情報と情報を紐付ける情報（XML, HTML, JSON）

***

### **追加チャレンジ**  加点要素とします

*   Postmanの「Tests」タブでレスポンス検証スクリプトを記述
*   JavaScript（axios）でSheetDB APIを呼び出す簡単なWebページを作成

***



