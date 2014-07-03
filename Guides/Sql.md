# VERVEコーディング規約(Sql)<a name="top"></a>

|Category|Element|
|:----:|---|
|テーブル設計|[テーブル命名規則](#name)
|基本ルール|[予約語の記述](#keyword)、[インデントと改行](#indent)、[コメント](#comment)、[結合条件](#join)
|DML|[SELECT句](#select)、 [UPDATE句](#update)、 [INSERT/REPLACE句](#insert)、 [WHERE句](#where)
|DDL|[CREATE TABLE](#create)、 [DROP TABLE](#drop)
　  
　  
　  
　  

> ## テーブル設計

　  

### ❏ テーブル命名規則<a name="name"></a>[【top】](#top)

- 半角英数字と`_`のみ使用可能です。
- 数字を安易に使用してはいけません。
- 全て小文字の`_`アンスコ区切りで命名して下さい。
- フレームワークに指定がある場合は、そちらを優先して下さい。

**良い例**

```sql
users
user_attributes
```

　  
　  
　  

> ## 基本ルール

　  

### ❏ 予約語の記述<a name="keyword"></a>[【top】](#top)

- 予約語は`大文字`で記述して下さい。

**良い例**
 
```SQL
SELECT column FROM tbl_name WHERE condition = '';
```

**悪い例**
 
```SQL
select column from tbl_name where condition = '';
```
　  
　  

### ❏ インデントと改行<a name="indent"></a>[【top】](#top)

- インデントはスペース`４つ`を使用して下さい。
- 基本的に、予約語・カラム・条件毎に改行しインデントして下さい。
- `,`や`AND`、`OR`は、行末に記述して下さい。
- ソース中にsqlを記述する場合は、`ヒアドキュメント`を使用して下さい。  
(言語毎の規約に規則がある場合はそちらを優先して下さい。)


**良い例**
 
```sql
SELECT 
    column1,
    column2 
FROM 
    tbl_name 
WHERE 
    condition1 = '' AND
    condition2 = '' AND
GROUP BY 
    column 
ORDER by 
    column DESC;


UPDATE 
    tbl_name
SET 
    column1 = 1, 
    column2 = 2 
WHERE
    condition1 = 1 AND
    condition2 = 1;
```

```php
$sql = >>>EOD
    SELECT 
        column
    FROM 
        tbl_name 
    WHERE 
        condition = '' 
        {$condition}
EDO;
```


**悪い例**
 
```php
$sql = 'SELECT column, '
      .'FROM tbl_name '
      .'WHERE condition = '' ';
```
　  
　  


- WHERE句等条件が動的に変わる場合は、sql中に言語のifで制御するのではなく  
先に定義して下さい。下記の例を参照。


**良い例**
 

```php
$condition1 = '';
$condition2 = '';

if ($isEnabledCondition1 == true) {
    $condition = ' AND condition1 = 1';
}
if ($isEnabledCondition2 == true) {
    $condition = ' AND condition2 = 2';
}

$sql = >>>EOD
    SELECT 
        column
    FROM 
        tbl_name 
    WHERE 
        condition = '' 
        {$condition1}
        {$condition2}
EDO;
```


**悪い例**
 
```php
$sql = >>>EOD
    SELECT 
        column
    FROM 
        tbl_name 
    WHERE 
        condition = '' 
EDO;

if ($isEnabledCondition1 == true) {
    $sql .= ' AND condition1 = 1';
}
if ($isEnabledCondition2 == true) {
    $sql .= ' AND condition2 = 2';
}
```
　  
　  

### ❏ コメント<a name="comment"></a>[【top】](#top)

- 一行のコメントは、`--`で記述して下さい。
- 複数行コメントは、`/**/`で記述して下さい。

**良い例**
 
```php
/* ○○を取得 */
SELECT 
    column1,    -- カラム１
    column2     -- カラム２
FROM 
    tbl_name 
WHERE 
    condition1 = '' AND
    condition2 = '' 
GROUP BY 
    column 
ORDER by 
    column DESC;

```

　  
　  


> ## DML

　  

### ❏ SELECT句<a name="select"></a>[【top】](#top)



- `(select * from )`は、使用しないで下さい。

**良い例**
 
```sql
SELECT
    column1, 
    column2
FROM
    tbl_name;
```

**悪い例**
 
```sql
SELECT * FROM tbl_name;
```
　  
　  
　  

### ❏ UPDATE句<a name="update"></a>[【top】](#top)


- 更新文が複数ある場合は、必ず改行して下さい。

**良い例**
 
```sql
UPDATE 
    tbl_name 
SET 
    column1 = 1, 
    column2 = 2;
```

**悪い例**
 
```sql
UPDATE tbl_name SET column1 = 1, column = 2;
```
　  
　  
　  

### ❏ INSERT/REPLACE句<a name="insert"></a>[【top】](#top)

- 予約語で改行し、要素はインデントして記述して下さい。
- SELECT INSERT の場合は、SELECT句部分は、SELECTの規約を参照して下さい。

**良い例**
 
```sql
INSERT INTO 
    ( column1, column2 )
VALUES
    ( val1, val2 );
```

**悪い例**
 
```sql
INSERT INTO ( column1, column2 )
VALUES ( val1, val2 );
```
　  
　  
　  

### ❏ WHERE句<a name="where"></a>[【top】](#top)

- 条件節が複数ある場合は、改行して記述して下さい。
- バインド変数を利用して下さい。

**良い例**
 
```sql
WHERE
    column1 = :condition1 AND
    column2 = :condition2 OR
    column3 = :condition3;
```

**悪い例**
 
```sql
WHERE
    column1 = 'condition1'
    AND column2 = 'condition2' 
    OR column3 = 'condition3';
```
　  
　  
　  

### ❏ 結合条件<a name="join"></a>[【top】](#top)

- テーブル結合の際は、テーブル名のエイリアスを定義して下さい。
- テーブル結合する際は、必ずテーブル毎・結合文毎に、  
テーブル結合に使用する予約語を先頭にして改行して下さい。

**良い例**
 
```php
FROM
    table1 AS t1, 
    table2 AS t2 

FROM
    table1 AS t1, 
    INNER JOIN table2 AS t2 ON t1.column1 = t2.column1
    INNER JOIN table3 AS t3 ON t1.column1 = t3.column1 
```

　  
　  


# DDL

> ## CREATE TABLE<a name="create"></a>[【top】](#top)

- `()`の中はインデントを入れて下さい。

**良い例**
 
```sql
CREATE TABLE IF NOT EXISTS tbl_name (
    id INT AUTO_INCREMENT,
    column1 VARCHAR(10) NOT NULL DEFAULT '',
    column2 VARCHAR(10) NOT NULL DEFAULT '',
    column3 VARCHAR(10) NOT NULL DEFAULT '',
    PRIMARY KEY (`id`),
    UNIQUE KEY `idx_1` (`column1 `),
    KEY `idx_1` (`column1`)
) ENGINE=InnoDB DEFAULT CHARSET=UTF8;
```


　  
　  
　  

> ## DROP TABLE<a name="drop"></a>[【top】](#top)


 
```php
DROP TABLE tbl_name;
```

  
　  
　  


　  
　  
　  
　  
　  
　  
　  
　  





