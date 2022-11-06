# README

## 株式会社iimon様 技術試験　サーバーサイド　C問題　提出物

**以下問題文**

- 下記の様に定義したテーブルがあります。ジャンルごとのitems.priceの平均値とジャンル名を取得したいと思っています
- どの様なクエリを発行するべきでしょうか？理由もつけて回答してください
- idカラム以外はインデックスを貼っていません。もし貼っておいた方が良いインデックスがあれば教えてください。こちらも理由をつけて回答してください

<img width="601" alt="スクリーンショット 2022-11-06 21 41 05" src="https://user-images.githubusercontent.com/87271490/200171335-487ee4f7-5d19-4517-8f0a-5ad077ac0216.png">  


**以下回答**

発行するクエリ
```
SELECT genres.name as 'ジャンル名', AVG(items.price) as '平均値'
FROM items INNER JOIN genres ON items.genre_id = genres.id 
GROUP BY genres.name;
```

想定している結果

|  ジャンル名  |  平均値  |
| ---- | ---- |
|  drink  |  350  |
|  fruit  |  98  |
|  vegetable  |  150  |


理由  
- itemsテーブルとgenresテーブルを結合するためにJOIN文を使う
- ジャンルごとにカテゴリ分けするためにGROUP BY文を使う
- ジャンルごとに分けられた状態で平均値を出すためにAVG文を使う

貼っておいた方が良いと考えるインデックス

インデックス名  
`items_name_id`

理由  
今後、「apple」や「potato」といった特定のレコードが何度も追加されることを想定したためです。  
itemsテーブルのnameカラムをIDに置き換え、item_nameテーブルを作成し、「apple」等の商品名はID化した方が管理しやすいかと考えました。