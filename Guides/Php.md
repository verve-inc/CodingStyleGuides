# VERVEコーディング規約(PHP)<a name="top"></a>


本文書は、VERVEでのコーディング規約を定めるものである。
　  

|Category|Element|
|:----:|---|
|[整形](#fairing)|[インデント](#indent)、[文字コード](#code)、[改行コード](#newline)、[1行の長さ](#length)|
|[リテラル](#literal)|[数値](#int)、[文字列](#string)、[論理値](#boolen)、[未定義値](#nil)、[ヒアドキュメント](#doc)|
|[演算子](#operator)|[算術演算子](#operator1)、[文字列結合演算子](#operator2)、[比較演算子](#operator3)、[論理演算子](#operator4)、[ビット演算子](#operator5)、[代入演算子](#operator6)、[三項演算子](#operator7)|
|[制御構文](#structure)|[条件式](#condition)、[if文](#if)、[for文](#for)、[while文](#while)、[foreach文](#foreach)、[switch文](#switch)、[try/catch文](#exeption)|
|[変数](#variable)|[ローカル変数](#localvar)、[グローバル変数](#globalvar)、[引数](#arg)、[配列](#array1)、[連想配列](#array2)|
|[定数](#const)|[ローカル/グローバル](#const1)、[enum](#enum)|
|[クラス](#class)|[定義](#class1)、[継承、実装](#class2)、[抽象クラス](#class3)、[利用](#class4)|
|[インターフェイス](#interface)|[定義](#interface1)|
|[プロパティ](#property)|[定義](#property1)、[抽象プロパティ](#property2)、[呼び出し](#property3)|
|[メソッド](#method)|[定義](#method1)、[抽象メソッド](#method2)、[呼び出し](#method3)|
|[関数](#function)|[ローカル](#function1)、[グローバル](#function2)、[ラムダ式(無名関数/クロージャ)](#lambda)|
|[名前空間](#namespace)|[定義](#namespace1)、[利用](#namespace2)|
|[コメント](#comment)|[ファイルコメント](#comment1)、[クラスコメント](#comment2)、[メソッドコメント](#comment3)、[関数コメント](#comment4)、[文中コメント](#comment5)|
|[特殊文字列](#spstring)|[コマンド呼び出し](#cmd)|
|[ファイル](#file)|[ファイル名](#filename)、[ファイルフォーマット](#format)|
　  
　  
　  
> ##  整形<a name="fairing"></a>[【top】](#top)

### ❏ インデント<a name="indent"></a>[【top】](#top)
`スペース４つ`を使用する。
　  
　  
### ❏ 文字コード<a name="code"></a>[【top】](#top)
`UTF-8`を使用する。
　  
　  
### ❏ 改行コード<a name="newline"></a>[【top】](#top)
`LF`を使用する。
　  
　  
### ❏ 1行の長さ<a name="length"></a>[【top】](#top)
ソフトリミットは`120文字`を上限とし、実際`100文字`以内に記述する。 
　  
　
> ## リテラル<a name="literal"></a>[【top】](#top)

### ❏ 数値<a name="int"></a>[【top】](#top)

- 整数

```php
$a = 1234; // 10進整数
$a = -123; // 負の数
$a = 0123; // 8進数 (10進数の83と等価)
$a = 0x1A; // 16進数 (10進数の26と等価)
$a = 0b11111111; // 2進数 (10進数の255と等価)

```

- 浮動小数点数

```php
$a = 1.234; 
$b = 1.2e3; 
$c = 7E-10;
```
　  
### ❏ 文字列<a name="string"></a>[【top】](#top)

- 文字列がリテラルである (変数の展開などが含まれない) 場合は、「シングルクォート」 で文字列を囲む。

```php
$a = '文字列の例';
```

- リテラル文字列自体にアポストロフィが含まれている場合は、
または、変数の展開を含む場合は引用符あるいは「ダブルクォート」で文字列を囲む。

```php
$sql = "SELECT `id`, `name` from `people` "
     . "WHERE `name`='Fred' OR `name`='Susan'";
```

- 変数の展開を行うには、次のような方法を使用する。

**良い例**
```php
$greeting = "こんにちは {$name} さん。ようこそ!";
```
　  
**悪い例**
```php
$greeting = 'こんにちは $name さん。ようこそ!';
```


### ❏ 論理値<a name="boolen"></a>[【top】](#top)

- 全て小文字で表記する。

**良い例**

```php
true
false
```

**悪い例**

```php
TRUE
FALSE
```
　  
　  
### ❏ 未定義値<a name="nil"></a>[【top】](#top)
- 全て小文字で表記する。

```php
null
```
　  
### ❏ ヒアドキュメント<a name="doc"></a>[【top】](#top)
- 変数展開を含まない限り、nowdoc構文を使用する。
- ラベル名は、全て大文字で、文字列の内容に合わせて命名する。
- 命名に迷う場合は EOF とする。

```php
$a = <<< 'EOF'
　　文字列
　　文字列
　　文字列
EOF
```

- 変数展開を含む場合、ダブルクォートでラベルを囲む。

```php
$a = <<< "EOF"
　　{$name}
　　文字列
　　文字列
EOF
```


　  
　  
> ## 演算子<a name="operator"></a>[【top】](#top)

### ❏ 算術演算子<a name="operator1"></a>[【top】](#top)
- 演算子の前後にはスペース１文字を入れる。

```php
 +        加算
 -        減算
 *        乗算
 /        除算
 %        剰余
```
　  
　  
### ❏ 文字列結合演算子<a name="operator2"></a>[【top】](#top)
- 演算子の前後にはスペース１文字を入れる。

- 文字列の連結には "." 演算子を使用する。
- コードを読みやすくするため、 "." 演算子の前後には常にスペースを入れる。

```php
$company = 'Zend' . ' ' . 'Technologies';
```
　  
- 文字列を "." 演算子で連結する際には、コードを読みやすくするために ひとつの文を複数行に分けることもできる。そのような場合は、 2 行目以降の行頭にスペースを入れ、各行の "." 演算子が最初の行の "=" 演算子と同じ位置にする。

```php
$sql = "SELECT `id`, `name` FROM `people` "
     . "WHERE `name` = 'Susan' "
     . "ORDER BY `name` ASC ";
```


### ❏ 比較演算子<a name="operator3"></a>[【top】](#top)

- 演算子の前後にはスペース１文字を入れる。

```php

$a === $b        // 等しい        $a が $b に等しく、および同じ型である場合に TRUE 。
$a !== $b        // 等しくない        $a が $b と等しくないか、同じ型でない場合に TRUE 。

$a == $b         // 等しい        型の相互変換をした後で $a が $b に等しい時に TRUE。
$a === $b        // 等しい        $a が $b に等しく、および同じ型である場合に TRUE 。
$a != $b         // 等しくない        型の相互変換をした後で $a が $b に等しくない場合に TRUE。
$a <> $b         // 等しくない        型の相互変換をした後で $a が $b に等しくない場合に TRUE。
$a !== $b        // 等しくない        $a が $b と等しくないか、同じ型でない場合に TRUE 。
$a < $b          // より少ない        $a が $b より少ない時に TRUE。
$a > $b          // より多い        $a が $b より多い時に TRUE。
$a <= $b         // より少ないか等しい        $a が $b より少ないか等しい時に TRUE。
$a >= $b         // より多いか等しい        $a が $b より多いか等しい時に TRUE。

```
　  
　  
### ❏ 論理演算子<a name="operator4"></a>[【top】](#top)

- 演算子の前後にはスペース１文字を入れる。
- 下記の記法を使用(論理積、論理和に and, or)は使用しない。


```php

&&              // 論理積
||              // 論理和
!               // 否定
xor             // 排他的論理和

$a and $b       // 論理積        $a および $b が共に TRUE の場合に TRUE
$a or $b        // 論理和        $a または $b のどちらかが TRUE の場合に TRUE
$a xor $b       // 排他的論理和        $a または $b のどちらかが TRUE でかつ両方とも TRUE でない場合に TRUE
!$a        　　// 否定        $a が TRUE でない場合 TRUE
$a && $b        // 論理積        $a および $b が共に TRUE の場合に TRUE
$a || $b        // 論理和        $a または $b のどちらかが TRUE の場合に TRUE

```
　  
　  
### ❏ ビット演算子<a name="operator5"></a>[【top】](#top)

- 演算子の前後にはスペース１文字を入れる。

```php

$a & $b        // 論理積。$aと$bの両方のビットが１の場合は１、それ以外は０
$a | $b        // 論理和。$aと$bの両方が０の場合は０、いづれかが１の場合は１
$a ^ $b        // 排他的論理和。$aと$bの片方が０で片方が１の場合は１。両方とも１または両方とも０の場合は０。
~$a            // 否定。$aの各ビットが、０の場合は１になり、１の場合は０になる。
$a << $b       // 左シフト。$a のビットを左に $b ビットシフトする。各シフトは "2を掛ける割る" ことになります。
$a >> $b       // 右シフト。$a のビットを右に $b ビットシフトする。各シフトは "2で割る" ことになります。

```

　  
### ❏ 代入演算子<a name="operator6"></a>[【top】](#top)

- 演算子の前後にはスペースを1文字入れる。

```php

+=              // 加算代入
-=              // 減算代入
*=              // 乗算代入
/=              // 除算代入
%=              // 剰余代入
.=              // 連結代入
++              // 加算子（インクリメント） 1加算して代入する
--              // 減算子（デクリメント） １減算して代入

$a &= $b        // 論理積で代入する。　$a = $a & $b と同じ。
$a |= $b        // 論理和で代入する。　$a = $a | $b と同じ。
$a ^= $b        // 排他的論理和で代入する。　$a = $a ^ $b と同じ。
$a <<= $b       // 左シフトで代入する。　$a = $a <<= $b と同じ。
$a >>= $b       // 右シフトで代入する。　$a = $a >>= $b と同じ。

```
　  
　  
### ❏ 三項演算子<a name="operator7"></a>[【top】](#top)

```php
（式１）?（式２）:（式３）        // 式１の結果がtrueの場合、式２を、falseの場合には式３を値にます。
```
　  
　  
> ##  制御構文<a name="structure"></a>[【top】](#top)

### ❏ 条件式<a name="condition"></a>[【top】](#top)

 - 制御構造キーワードの後には１スペースを設ける。
 - 開き括弧の後にスペースを配置する。
 - 閉じ括弧の前にスペースを配置するべきではない。
 - 開き括弧と閉じ中括弧の間にはスペースを挟む。
 - 構造本文は１インデント下げる。
 - 閉じ括弧は構造本文の後に改行して配置する。

 
### ❏ if文<a name="if"></a>[【top】](#top)

- else elseif とブレースは同じ行に記述する。
- else if ではなく elseif を使う。

```php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```
　  
### ❏ for文<a name="for"></a>[【top】](#top)


```php
for ($i = 0; $i < 10; $i++) {
    // for body
}

```
　  
　  
### ❏ while文<a name="while"></a>[【top】](#top)


```php
while ($expr) {
    // structure body
}

```
　  
　  
### ❏ foreach文<a name="foreach"></a>[【top】](#top)

```php
foreach ($iterable as $key => $value) {
    // foreach body
}
```
　  
　  
### ❏ switch文<a name="switch"></a>[【top】](#top)

- case文はswitchからインデントし、break（またはその他の終端キーワード）は、case内本文と同じレベルのインデントで揃える。 また意図的に処理スルーさせる場合は「// no break」等、コメントする。

```php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```


　 
### try/catch文<a name="exeption"></a>[【top】](#top)

```php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```
　  
　  
> ## 変数<a name="variable"></a>[【top】](#top)

### ❏ ローカル変数<a name="localvar"></a>[【top】](#top)

- 変数名に含めることができるのは英数字のみです。 アンダースコアを使用してはならない。
- 数字を安易に使用してはならない。
- 常に小文字で開始する "camelCaps" 方式を使用する。
- "$i" や "$n" のような変数が許されるのは、小さなループ内で使用するのみ。 
　  
　  

### ❏ グローバル変数<a name="globalvar"></a>[【top】](#top)

[ローカル変数](#localvar)と同様の規則です。　  
　  
　  
### ❏ 引数<a name="arg"></a>[【top】](#top)

[ローカル変数](#localvar)と同様の規則です。
　  
　  
### ❏ 配列<a name="array1"></a>[【top】](#top)

- 配列を使用する前に、array() を用いて配列型を宣言する。
- 配列に要素を指定する場合、カンマ区切りの直後に 1 つの空白記号を入れる。
- PHP 5.4.0 以降の配列の短縮構文は、まだ使用しない。

　  
　  
### ❏ 連想配列<a name="array2"></a>[【top】](#top)

- 連想配列を Array で宣言する場合には、配列の最初の要素を次の行から始める。 配列を宣言した位置からさらに一段インデントした位置で要素をそろえ、 それ以降のすべての要素を同じインデントで記述する。 閉じ括弧はそれ単体でひとつの行に記述し、インデント量は配列の宣言と同じ位置となる。 
- 可読性を高めるため、代入演算子 "=>" の位置はそろえておく。

```php
$sampleArray = array(
    'firstKey'  => 'firstValue',
    'secondKey' => 'secondValue',
);
```
- ※PHP 5.4.0 以降の配列の短縮構文は、まだ使用しないでください。　  
　  
　  

> ## 定数<a name="const"></a>[【top】](#top)

### ❏ ローカル/グローバル<a name="const1"></a>[【top】](#top)

- 全て大文字とし、区切り文字にはアンダースコアを用いて定義する。

　  
### ❏ enum<a name="enum"></a>[【top】](#top)

- phpの言語仕様にありません。
　  

　  
> ## クラス<a name="class"></a>[【top】](#top)

### ❏ 定義<a name="class1"></a>[【top】](#top)

- クラス名は大文字から始める。
       
```php
class Whisky
```

- 複数の単語を組み合わせたクラス名を使用する場合は、それぞれの単語の 1 文字目を大文字にする。

```php
class SingleMaltWhisky
```

- クラスの開き括弧は次の行に記述しなければなりません。また閉じ括弧は本文最後の次の行に記述する。

```php
class SingleMaltWhisky
{
}
```
　  
　  
### ❏ 継承、実装<a name="class2"></a>[【top】](#top)

- extendsとimplementsは、クラス名と同じ行で定義する。

```php
pirit extends Alcohol implements Distilling
```

- mplements 定義は、インデントにより揃えることで、複数行に分割する。
      その際、最初の定義も次の行からはじめるものとし、１行に１つのインターフェイスを定義する。  

```php

class Whisky extends Alcohol implements
     Distilling,
     Aging,
     Bottling
{
}

```
　  
　  
### ❏ 抽象クラス<a name="class3"></a>[【top】](#top)

- ※クラスの(定義, 継承、実装)と同様
　  
　  

### ❏ 利用<a name="class4"></a>[【top】](#top)

```php
//親クラス（抽象クラス）  
abstract class ParentClass {  
    public function ParentMethod(){  
        print('ParentMethod</br>');  
    }  
}

//子クラス  
class ChildClass extends ParentClass{  
}

```
　  
> ## インターフェイス<a name="interface"></a>[【top】](#top)

### ❏ 定義<a name="interface1"></a>[【top】](#top)

- ※クラスの(定義, 継承、実装)と同様
　  

　  
> ## プロパティ<a name="property"></a>[【top】](#top)

### ❏ 定義<a name="property1"></a>[【top】](#top)

- var 構文を使用しない。
- メンバ変数を宣言する際には private、protected あるいは public のいずれかの修飾子を用いてアクセス範囲を指定する。

- 変数名に含めることができるのは英数字のみです。 アンダースコアを使用しない。
- 数字を安易に使用しない。
- 常に小文字で開始する "camelCaps" 方式を使用しない。
　  

　  
### ❏ 抽象プロパティ<a name="property2"></a>[【top】](#top)

- phpの言語仕様にありません。
　  

　  
### ❏ 呼び出し<a name="property3"></a>[【top】](#top)

```php
$object -> propetyName
```

　  
> ## メソッド<a name="method"></a>[【top】](#top)

### ❏ 定義<a name="method1"></a>[【top】](#top)

- メソッド名に含めることができるのは英数字のみ。 アンダースコアを使用しない。
- 数字を安易に使用しない。
- 常に小文字で開始する "camelCaps" 方式を使用しない。
- 常に private、protected あるいは public のいずれかの修飾子を用いてアクセス範囲を指定する。

- 関数名と引数定義用の開始括弧の間にはスペースを入れない。
- 開始括弧は関数名と同じ行に記述する。

```php
☓
public function func1() {
}; 

☓ 
public function func2() {
};

☓
public function func3() {
};

○
public function start() {
};

```
　  
　  
### ❏ 抽象メソッド<a name="method2"></a>[【top】](#top)
- メソッドにabstract修飾子をつけると、そのメソッドはサブクラスで必ずオーバーライドする。
- abstractメソッドを定義しているクラスはabstract修飾子をつける。
- abstractメソッドはメソッド定義だけを宣言し、処理内容は定義しない。
- abstractメソッドをオーバーライドした際のアクセス修飾子は、abstractメソッドで定義した修飾子より同じか緩くする必要がある。
- たとえばprotectedで定義したabstractメソッドをオーバーライドするときは、protectedまたはpublicにする。
- abstractメソッドをオーバーライドしたとき、引数はabstractメソッドと同じにするか、省略可能な引数を追加することが可能となる。

```php
//abstractメソッドはメソッド定義だけを宣言し、処理内容は定義しない。  
protected abstract function AbstractMethod($value); 
```
　  
　  
### ❏ 呼び出し<a name="method3"></a>[【top】](#top)

- 関数の引数を指定する際は、引数を区切るカンマの後に空白をひとつ入れる。 
- 引数が多い(または引数として与える変数名、文字列が長い)ため、一行の文字数の上限を超える場合は、
- 引数１つ毎に改行します。その際、引数の前に空白を埋め、引数の位置を揃える。
- 引数リストの閉じ括弧は、最後の引数の次の行に、開き括弧との位置を揃えて記述する。


```php
func($name,
        $longName,
        $longLongName,
        $longLongLongName
        );
```
　  
　  
> ## 関数<a name="function"></a>[【top】](#top)

### ❏ ローカル<a name="function1"></a>[【top】](#top)

- 半角英数字のみ使用可能とする。
- 数字は安易に使用しない。
- 小文字で開始する`camelCaps方式`で記述する。

**良い例**

```php
function start() {
}
```　  
　  
### ❏ グローバル<a name="function2"></a>[【top】](#top)

- 関数名に含めることができるのは英数字のみ可能とする。 アンダースコアを使用しない。
- 数字を安易に使用しない。

```php
☓
function func1() {
}; 

☓ 
function func2() {
};

☓
function func3() {
};

```
　  

- 常に小文字で開始する "camelCaps" 方式を使用する。

- 関数名と引数定義用の開始括弧の間にはスペースを入れない。
- 開始括弧は関数名と同じ行に記述する。

**良い例**

```php

function start() {
}

```
　  
### ❏ ラムダ式(無名関数/クロージャ)<a name="lambda"></a>[【top】](#top)

```php

$result = array_map($array, function($value) { return $value * 2; });

$result = array_map($array, hoge);
hoge($value) {
  return $value * 2;
}

```
　  
　  
> ## 名前空間<a name="namespace"></a>[【top】](#top)

### ❏ 定義<a name="namespace1"></a>[【top】](#top)

- 名前空間の定義の後に空行が必要となる。
- use定義は、名前空間宣言の後でなければならない。
- 定義ごとにuse演算子が必要となる。
- use定義のブロックの後には空行が必要となる。

　  
### ❏ 利用<a name="namespace2"></a>[【top】](#top)

```php
namespace foo;
use My\Full\Classname as Another;

// これは use My\Full\NSname as NSname と同じです
use My\Full\NSname;

// グローバルクラスをインポートします
use ArrayObject;

$obj = new namespace\Another; // foo\Another クラスのオブジェクトのインスタンスを作成します
$obj = new Another; // My\Full\Classname クラスのオブジェクトのインスタンスを作成します
NSname\subns\func(); // My\Full\NSname\subns\func 関数をコールします
$a = new ArrayObject(array(1)); // ArrayObject クラスのオブジェクトのインスタンスを作成します
// "use ArrayObject" がなければ、foo\ArrayObject クラスのオブジェクトのインスタンスを作成することになります

```
　  
　  
> ## コメント<a name="comment"></a>[【top】](#top)

### ❏ ファイルコメント<a name="comment1"></a>[【top】](#top)

- C 言語形式 (/* */) と標準 C++ コメント (//) のどちらも使用可能とする。 Perl/shell 形式のコメント (#) は使用するべきでない。

- 単一のクラス定義を記述したファイルの場合は不要とする。

```php
/**
* ファイルについての短い説明
*
* ファイルについての長い説明 (もしあれば)...
*
* @author 作った人
*/
```
　  
　  
### ❏ クラスコメント<a name="comment2"></a>[【top】](#top)

- C 言語形式 (/* */) と標準 C++ コメント (//) のどちらも使用可能とする。 Perl/shell 形式のコメント (#) は使用するべきでない。
- 
```php
/**
* クラスについての短い説明
*
* クラスについての長い説明 (もしあれば)...
*
* @author 作った人
*/
```
　  
### ❏ メソッドコメント<a name="comment3"></a>[【top】](#top)

- C 言語形式 (/* */) と標準 C++ コメント (//) のどちらも使用可能とする。 Perl/shell 形式のコメント (#) は使用するべきでない。

```php
/**
* aaaの説明
*
* @param string $arg 第一引数
* @param integer $arg2 第二引数
* @return array 戻り値の説明
*/
function aaa($arg,$arg2) {
}

```
　  
　  
### ❏ 関数コメント<a name="comment4"></a>[【top】](#top)

- C 言語形式 (/* */) と標準 C++ コメント (//) のどちらも使用可能とする。 Perl/shell 形式のコメント (#) は使用するべきでない。

```php
/**
* aaaの説明
*
* @param string $arg 第一引数
* @param integer $arg2 第二引数
* @return array 戻り値の説明
*/
function aaa($arg,$arg2) {
}

```
　  
　  
### ❏ 文中コメント<a name="comment5"></a>[【top】](#top)

- C 言語形式 (/* */) と標準 C++ コメント (//) のどちらも使用可能とする。 Perl/shell 形式のコメント (#) は使用するべきでない。
　  
　  

> ## 特殊文字列<a name="spstring"></a>[【top】](#top)


### ❏ コマンド呼び出し<a name="cmd"></a>[【top】](#top)

- exec()関数を推奨

```php

exec($cmd . " > /dev/null &");

```

　  
> ## ファイル<a name="file"></a>[【top】](#top)

### ❏ ファイル名<a name="filename"></a>[【top】](#top)

- フレームワークにより規定されている場合はそちらを優先　  
　  
### ❏ ファイルフォーマット<a name="format"></a>[【top】](#top)

