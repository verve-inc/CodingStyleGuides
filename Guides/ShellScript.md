#VERVEコーディング規約雛形

## 概要

本文書は、VERVEでのShellScriptプログラムにおけるコーディング規約を定めるものである。


> ## 整形 <a name="fairing"</a>[【top】](#top)

### インデント<a name="indent"></a>[【top】](#top)
`スペース4つ`を使用します。

### 文字コード<a name="code"></a>[【top】](#top)
`UTF-8`を使用します。

### 改行コード<a name="newline"></a>[【top】](#top)
`LF`を使用します。

### 1行の長さ<a name="length"></a>[【top】](#top)
1行が`100文字`を超えないようにします。`100文字`を超える場合は、適宜改行を入れます。

> ## リテラル<a name="fairing"</a>[【top】](#top)


### 数値

### 文字列

### 論理値

### 未定義値

### ヒアドキュメント<a name="doc"></a>[【top】](#top)

**良い例**
- ヒアドキュメントで使用する文字列はEOFを優先して使用する

```bash
cat << EOF
test1
test2
test3
EOF
```

**悪い例**

```bash
cat << hoge
test1
test2
test3
hoge
```

> ## 演算子<a name="operator"></a>[【top】](#top)

### 算術演算子<a name="operator1"></a>[【top】](#top)

- 算術演算の評価は「(())」で可能だが、数値演算はexprコマンドを優先的に使用する、また条件判断はtestコマンド（[]）を優先的に使用する

**良い例**
```bash
i=1
while [ "$i" -le 10 ]
do
  echo "$i";
  i=`expr "$i" + 1`
done
```

**悪い例**
```bash
i=1
while ((i <= 10))
do
  echo "$i";
  ((i++))
done
```

### 文字列結合演算子<a name="operator2"></a>[【top】](#top)
- 文字列結合演算子は仕様には存在しないが、変数との結合時は中括弧「{}」で変数部分を囲むこと

**良い例**
```bash
STRING1=xyz
VAR=abc${STRING1}
````

**悪い例**
```bash
STRING1=xyz
VAR=abc$STRING1
````

### 比較演算子<a name="operator3"></a>[【top】](#top)
- 文字列の比較は「==」ではなく「=」を使用する

**良い例**
```bash
STRING1=abc
if [ "$STRING1" = "abc" ]; then
````

**悪い例**
```bash
STRING1=abc
if [ "$STRING1" == "abc" ]; then
````

### 論理演算子<a name="operator4"></a>[【top】](#top)
- 両方が真の場合に使用する「&&」と「-a」では「&&」を優先的に使用する
どちらかが真の場合に使用する「||」と「-o」では「||」を優先的に使用する


**良い例**
```bash
STRING1=abc
STRING2=xyz
if [ "$STRING1" = "abc" ] && [ "$STRING2" = "xyz" ]; then
    echo "$STRING1"
    echo "$STRING2"
fi
````

**悪い例**
```bash
STRING1=abc
STRING2=xyz
if [ "$STRING1" = "abc" -a "$STRING2" = "xyz" ]; then
    echo "$STRING1"
    echo "$STRING2"
fi
````

### ビット演算子<a name="operator5"></a>[【top】](#top)
- AND("&")、OR("|")、XOR("^")、シフト("<<", ">>")の前後には、スペース１文字を入れる。

**良い例**
```bash
i=10
test=$(( i << 1 ))
````

**悪い例**
```bash
i=10
test=$((i<<1))
````

### 代入演算子<a name="operator6"></a>[【top】](#top)
- コマンド置換の結果を代入する際は、「$()」より「`」を優先して使う

**良い例**
```bash
cmd=`ls -l | awk '{print $9}'`
````

**悪い例**
```bash
cmd=$(ls -l | awk '{print $9}')
````

### 三項演算子<a name="operator7"></a>[【top】](#top)
- 演算子「?」、「:」の前後にスペース１文字を入れる。

**良い例**
```bash
num1=2;
num2=5;
echo $(($num1 > $num2 ? $num1 : $num2))
````

**悪い例**
```bash
num1=2;
num2=5;
echo $(($num1 > $num2?$num1:$num2))
````

> ##  制御構文<a name="structure"></a>[【top】](#top)

### 条件式<a name="condition"></a>[【top】](#top)

### if文<a name="if"></a>[【top】](#top)

- ifとthenは同一行に記載する

**良い例**
```bash
STRING1=abc
if [ "$STRING1" = "abc" ]; then
　　echo "$STRING1"
fi
````

**悪い例**
```bash
STRING1=abc
if [ "$STRING1" = "abc" ]
then
　　echo "$STRING1"
fi
````

### for文<a name="for"></a>[【top】](#top)
- doは改行しdoneと頭を揃えること

**良い例**
```bash
for ((i = 1; i <=10; i++))
do
　　echo "$i"
done
````

**悪い例**
```bash
for ((i = 1; i <= 10; i++)); do
　　echo "$i"
done
````

### while文<a name="while"></a>[【top】](#top)
- doは改行しdoneと頭を揃えること

**良い例**
```bash
i=1
while [ "$i" -le 10 ]
do
    echo "$i"
    i=`expr "$i" + 1`
done
````

**悪い例**
```bash
i=1
while [ "$i" -le 10 ]; do
    echo "$i"
    i=`expr "$i" + 1`
done
````

### foreach文<a name="foreach"></a>[【top】](#top)

- doは改行しdoneと頭を揃えること

**良い例**
```bash
for i in web db mail
do
    echo "$i"
done
````

**悪い例**
```bash
for i in web db mail; do
    echo "$i"
done
````

### switch文<a name="switch"></a>[【top】](#top)


> ## 変数<a name="variable"></a>[【top】](#top)

### ローカル変数<a name="localvar"></a>[【top】](#top)

- 変数名はすべて小文字で、単語のつなぎ目は「_ 」にする

**良い例**
```bash
func () {
  local backup_dir=$1
}
````

**悪い例**
```bash
func () {
  local backupdir=$1
}
````

### グローバル変数<a name="globalvar"></a>[【top】](#top)

- 変数名はすべて小文字で、単語のつなぎ目は「_ 」にする

**良い例**
```bash
BACKUP_DIR="/backup"
````

**悪い例**
```bash
BackupDir="/backup"
````

### 引数<a name="arg"></a>[【top】](#top)

- 変数名はすべて小文字で、単語のつなぎ目は「_ 」にする

**良い例**
```bash
BACKUP_DIR="/backup"
````

**悪い例**
```bash
BackupDir="/backup"
````

### 配列<a name="array1"></a>[【top】](#top)

- 変数名はすべて小文字で、単語のつなぎ目は「_ 」にする

**良い例**
```bash
ARRAY_HOST=(web db mail dns)
````

**悪い例**
```bash
arrayhost=(web db mail dns)
````

### 連想配列<a name="array2"></a>[【top】](#top)

- Bash 4以降のみ利用可能

> ## 定数<a name="const"></a>[【top】](#top)

### ローカル/グローバル<a name="const1"></a>[【top】](#top)

- 変数名の頭は「 _ 」をつけ、大文字を使用し単語のつなぎ目は「 _ 」にする


**良い例**
```bash
readonly _BACKUP_DIR="/backup"
````

**悪い例**
```bash
readonly BACKUP_DIR="/backup"
````

> ## 関数<a name="function"></a>[【top】](#top)

### ローカル<a name="function1"></a>[【top】](#top)

### グローバル<a name="function2"></a>[【top】](#top)

## コメント

### ファイルコメント


### 関数コメント

### 文中コメント


## 特殊文字列

### コマンド呼び出し


## ファイル

### ファイル名
