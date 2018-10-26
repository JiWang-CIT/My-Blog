---
title: JSON紹介
description: PythonでのJSON利用についてまとめてみた．
date: 2018-10-26 15:11:19
categories:
 - Tutorial
tags: Python, JSON
---


![JSON vector logo.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/JSON_vector_logo.svg/160px-JSON_vector_logo.svg.png)

## What's JSON

>  JSON, short for **J**ava**S**cript **O**bject **N**otation, is an open-standard file format that uses human-readable text to transmit data objects, used as a replacement for XML in some AJAX-style systems.
>
> <p align="right">-- Wikipedia</p>

 軽量なデータ記述言語の1つである。構文はJavaScriptにおけるオブジェクトの表記法をベースとしているが、JSONはJavaScript専用のデータ形式では決してなく、様々なソフトウェアやプログラミング言語間におけるデータの受け渡しに使えるよう設計されている。

以前，インターネットに渡ってデータを受け渡しする際によく使われた記述言語はXMLである．しかし，XMLの構文構造が複雑であり，軽量化したJSONの時代が来た．

JSONの文字コードはUTF-8となることで，どのプラットフォームでもちゃんと動かせるメリットもある．

## JSONの文法規則

1. データ構造：**名前／値**　のペア構造．両者が一対一でコロン「`:`」で区切る
2. データの間いにカンマ 「`,`」 で区切る．
3. オブジェクトは中括弧「`{}`」で囲む
4. 配列は大括弧(ブラケット)「`[]`」で囲む
5. 文字列はダブルクォーテーション「`""`」で囲む

### データの書き方例

``` JSON
{
    "name" : "Jason",
    "age" : 18,
    "marriage" : false,

    "nickname" : [  // 文字列配列
        "アイウエオ",
        "qwert",
        "测试用文字列" // 最後にカンマが要らない
    ]，

    "bookList": [  // オブジェクト配列
        {"title" : "Pride and Prejudice",   "price" : 20},
        {"title" : "History of the America",   "price" : 40}
    ]        
}
```


## PythonでのJSON利用

Pythonでは，JSON利用のためのpackageがある

``` python
import json
```



| 関数         | 紹介                                 |
| ------------ | ------------------------------------ |
| `json.dumps` | PythonオブジェクトをJSON文字列に変換 |
| `json.loads` | JSON文字列をPythonオブジェクトに変換 |

### `json.dumps`の例

文法：

```python
json.dumps(obj, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, encoding="utf-8", default=None, sort_keys=False, **kw)
```

使用例：
``` python
import json

data = [ { 'a' : 1, 'b' : 2, 'c' : 3, 'd' : 4, 'e' : 5 } ]

json = json.dumps(data)
print (json)

print (json.dumps({'a': 'lakjf', 'b': 6}, sort_keys=True, indent=4, separators=(',', ': ')))
```

上記コードの実行結果は：

``` json
[{"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}]
{
    "a": "lakjf",
    "b": 6
}
```



### `json.loads`の例

文法：

```python
json.dumps(obj, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, encoding="utf-8", default=None, sort_keys=False, **kw)
```

使用例：

```python
import json

jsonData = '{"a":1,"b":2,"c":3,"d":4,"e":5}';

text = json.loads(jsonData)
print (text)
```

上記コードの実行結果は：

```python
{'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}
```



## 補足

PythonでのJSON利用について，`demjson`というサードパーティ製のpackageがある．公式サイトは　http://deron.meranda.us/python/demjson/

### Quick example (code) via Official Site

```python
>>> import demjson

>>> demjson.encode( ['one',42,True,None] )    # From Python to JSON
'["one",42,true,null]'

>>> demjson.decode( '["one",42,true,null]' )  # From JSON to Python
['one', 42, True, None]

>>> cfg = demjson.decode_file( "config.json" )  # Read JSON from a file
```
