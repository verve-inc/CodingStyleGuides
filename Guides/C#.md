# VERVEコーディング規約(C#)<a name="top"></a>

本文書は、VERVEでのC#プログラムにおけるコーディング規約を定めるものである　  

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
`スペース4つ`を使用します。

### ❏ 文字コード<a name="code"></a>[【top】](#top)
`UTF-8`を使用します。

### ❏ 改行コード<a name="newline"></a>[【top】](#top)
`LF`を使用します。

### ❏ 1行の長さ<a name="length"></a>[【top】](#top)
1行が`100文字`を超えないようにします。`100文字`を超える場合は、適宜改行を入れます。


> ## リテラル<a name="literal"></a>[【top】](#top)

### ❏ 数値<a name="int"></a>[【top】](#top)

整数

```csharp
int i = 1;
```

小数

- 小数は、数値の後ろに`f`を付与します。

```csharp
float distance = 0.5f;
```

16進数

- 16進数は、数値の前に`0x`を付与して、`a`〜`f`は小文字で記述します。

```csharp
int address = 0xff3c;
```


### ❏ 文字列<a name="string"></a>[【top】](#top)

- 文字列は、二重引用符`(" ")`で囲まれる文字の系列です。  
文字列中では、以下のエスケープシーケンスを用いることができます。

```csharp
\n  // 改行
\t  // 水平タブ
\r  // 復帰
\v  // 垂直タブ
\a  // ベル
\b  // 一文字後退
\f  // フォームフィード
\\  // バックスラッシュ
\"  // 二重引用符 (")
\'  // 一重引用符 (')
\uXXXX // Unicode文字
```

- 長い文字列で1行の長さの制限を超える場合は、結合演算子を使って改行します。

```csharp
string longString = "012...789"
    + "012...789"
    + "012...789";
```


### ❏ 論理値<a name="boolen"></a>[【top】](#top)

- 全て小文字で表記します。

**良い例**

```csharp
bool isFinished = true;
bool isInField = false;
```

**悪い例**

```csharp
bool isFinished = TRUE;
bool isInField = FALSE;
```


### ❏ 未定義値<a name="nil"></a>[【top】](#top)

- 全て小文字で表記します。

```csharp
SomeClass instance = null;
```


### ❏ ヒアドキュメント<a name="doc"></a>[【top】](#top)

- C#の言語仕様にありません。


> ## 演算子<a name="operator"></a>[【top】](#top)

### ❏ 算術演算子<a name="operator1"></a>[【top】](#top)

- `+`、`-`、`*`、`/`、`%`の前後にはスペース1文字を入れます。

**良い例**

```csharp
int a = 1 + 1;
int b = 2 - 1;
int c = 2 * 3;
float d = 5.0f / 2.0f;
int d = 10 % 3;
```

**悪い例**

```csharp
int a = 1+1;
int b = 2-1;
int c = 2*3;
float d = 5.0f/2.0f;
int d = 10%3;
```

- インクリメント`++`、デクリメント`--`と変数の間にはスペースは入れません。

**良い例**

```csharp
i++;
--j;
```

**悪い例**

```csharp
i ++;
-- j;
```

 
### ❏ 文字列結合演算子<a name="operator2"></a>[【top】](#top)

- 文字列結合演算子の前後にはスペース1文字を入れます。

**良い例**

```csharp
string userId = "abc" + "123";
```

**悪い例**

```csharp
string userId = "abc"+"123";
```

- 折り返す場合は"+"の前に改行を入れ、2行目以降はインデントを1つ下げます。

**良い例**

```csharp
string longString = "012...789"
    + "012...789"
    + "012...789";
```

**悪い例**

```csharp
string longString = "012...789"
+ "012...789";
string longString = "012...789"
                  + "012...789";
```


### ❏ 比較演算子<a name="operator3"></a>[【top】](#top)

- 比較演算子は変数を左に、リテラルを右に置きます。また、比較演算子の前後には、スペース1文字を入れます。

**良い例**

```csharp
if (i > 0) {
}
```

**悪い例**

```csharp
if (true == isFinished) {
}
if (i>0) {
}
```


### ❏ 論理演算子<a name="operator4"></a>[【top】](#top)

- 論理演算子の前後には、スペース1文字を入れます。

**良い例**

```csharp
return (a == 1) && (b == 2);
```

**悪い例**

```csharp
return (a == 1)&&(b == 2);
```


### ❏ ビット演算子<a name="operator5"></a>[【top】](#top)

- AND(`&`)、OR(`|`)、XOR(`^`)、シフト(`<<`, `>>`)の前後には、スペース1文字を入れます。

**良い例**

```csharp
i = i & 0x11;
```

**悪い例**

```csharp
i = i&0x11;
```

- NOT("~")と変数の間には、スペースを入れません。

**良い例**

```csharp
i = ~i;
```

**悪い例**

```csharp
i = ~ i;
```


### ❏ 代入演算子<a name="operator6"></a>[【top】](#top)

- 代入演算子の前後には、スペース1文字を入れます。

**良い例**

```csharp
i = 1;
i += 1;
```

**悪い例**

```csharp
i=1;
i+=1;
```


### ❏ 三項演算子<a name="operator7"></a>[【top】](#top)

- 三項演算子の前後には、スペース1文字を入れます。

**良い例**

```csharp
string extension = (type != null) ? extensionDictionary[type] : "txt";
```

**悪い例**

```csharp
string extension = (type != null)?extensionDictionary[type]:"txt";
```

- 途中で行を折り返す場合は演算子の前に改行を入れ、2行目以降はインデントを1つ下げます。

**良い例**

```csharp
string extension = (type != null)
    ? extensionDictionary[type]
    : "txt";
```

**悪い例**

```csharp
string extension = (type != null)
? extensionDictionary[type]
: "txt";
```


> ##  制御構文<a name="structure"></a>[【top】](#top)

### ❏ 条件式<a name="condition"></a>[【top】](#top)

- 条件式を囲う括弧の前後にはスペース1文字を入れます。
- 条件式を囲う括弧と条件式との間にはスペースを入れません。
- 開き波括弧`{`は条件式と同じ行に記述します。
- 閉じ波括弧`}`の前で改行を入れ、インデントの深さは条件文と揃えます。
- 波括弧を省略できる場合でも、波括弧を省略してはいけません。

**良い例**

```csharp
if (i == 0) {
    // Do something.
}
```

**悪い例**

```csharp
if( i == 0 ){
    // 条件式の前後にスペースが入ってしまっている。
}

if (i == 0)
{
    // 開き波括弧は条件式と同じ行に無い。
}

if (i == 0) {
    // 閉じ波括弧のインデントが揃っていない。
    }

if (i == 0) text = "The number is zero.";
// 波括弧を省略してしまっている。
```

### ❏ if文<a name="if"></a>[【top】](#top)

- `else`、`else if`は、閉じ波括弧`}`の後にスペース1文字を空けて記述します。

**良い例**

```csharp
if (i == 0) {
    text = "No.0";
} else if (i == 1) {
    text = "No.1";
} else {
    text = "Out of the range";
}
```

**悪い例**

```csharp
if (i == 0) {
    text = "No.0";
}
else if (i == 1) {
    text = "No.1";
}else{
    text = "Out of the range";
}
```

### ❏ for文<a name="for"></a>[【top】](#top)

- 条件式に記述するセミコロン`;`の前にはスペースを入れず、後にはスペース1文字を入れます。

**良い例**

```csharp
for (int i = 0; i < 10; i++) {
    // Do something.
}
```

**悪い例**

```csharp
for (int i = 0 ;i < 10 ;i++) {
    // Do something.
}
```


### ❏ while文<a name="while"></a>[【top】](#top)

- 条件をループ処理の前に記述する場合は以下のように記述します。

```csharp
while (i < 10) {
    i++;
}
```

- 条件をループ処理の後に記述する場合は、`do`を使って記述します。
- 開き波括弧`{`は`do`と同じ行に記述し、`do`との間にスペース1文字を入れます。
- `while`は閉じ波括弧`}`と同じ行に記述し、閉じ波括弧との間にスペース1文字を入れます。

**良い例**

```csharp
do {
    i++;
} while (i < 10);
```

**悪い例**

```csharp
do
{
    i++;
}
while (i < 10);
```


### ❏ foreach文<a name="foreach"></a>[【top】](#top)

```csharp
foreach (string value in valueList) {
}
```


### ❏ switch文<a name="switch"></a>[【top】](#top)

- `case`は`switch`より1つインデントを下げます。
- `case`の中身の処理文は、`case`より1つインデントを下げます。

**良い例**

```csharp
switch (i) {
    case 0:
        text = "0です。";
        break;
}
```

**悪い例**

```csharp
switch (i) {
case 0:
text = "0です。";
break;
}
```

- 意図的に`break`を省略する場合は、コメントで`// No break`を記述します。(何も書かれていないと、後から読んだ人は本当に必要ないのか書き忘れなのか判断をつけにくいため。)
- `default`句を省略してはいけません。
- `default`句で何も処理する必要がない場合は、コメントで`// Do nothing`と記述します。(`default`句が省略されていたり、中身に何も書かれていないと、後から読んだ人は本当に必要ないのか書き忘れなのか判断をつけにくいため。)
- 一番下に記述する`case`句も、`break`を省略しないで記述します。(後に`case`句が追加された時に、`break`の書き忘れによってバグが発生するのを防ぐため。)
- `default`句は`case`句の下に記述します。

**良い例**

```csharp
switch (i) {
    case 0:
        text = "No.0";
        // No break
    case 1:
        text += "No.1";
        break;
    default:
        // Do nothing
        break;
}
```

**悪い例**

```csharp
switch (i) {
    default: // default句はcase句の下に来ていない。
        break; // "Do nothing"の記述が無い。
    case 0:
        text = "0 ";
        // "No break"の記述が無い。
    case 1:
        text += "1 ";
        // breakが無い。
}
```

### try/catch文<a name="exeption"></a>[【top】](#top)

- 開き波括弧`{`は`try`と同じ行に記述し、`try`との間にスペース1文字を入れます。
- `catch`の前の閉じ波括弧`}`、後の開き波括弧`{`は`catch`と同じ行に記述し、catchと波括弧との間にスペース1文字を入れます。

**良い例**

```csharp
try {
    // Do something
} catch (Exception e) {
    // Do something
}
```

**悪い例**

```csharp
try
{
    // Do something
}
catch (Exception e)
{
    // Do something
}
```


> ## 変数<a name="variable"></a>[【top】](#top)

### ❏ ローカル変数<a name="localvar"></a>[【top】](#top)

- 変数名はキャメルケース(先頭は`英小文字`、後続の単語の先頭は`英大文字`)で記述します。

**良い例**

```csharp
int resourceMapIndex = 0;
```

**悪い例**

```csharp
int ResourceMapIndex = 0;
int resource_map_index = 0;
```

### ❏ グローバル変数<a name="globalvar"></a>[【top】](#top)

- C#の言語仕様にありません。
- 擬似的に、クラスの外部から参照可能な変数をグローバル変数のように扱う事ができます。この場合は、staticプロパティとして定義します。

```csharp
public class GlobalConfig {
    // staticプロパティとして定義する
    public static int soundVolume = 100;
}

public class Main {
    public Main() {
        // クラス外のどこからでも参照・更新が可能
        GlobalConfig.soundVolume = 50;
    }
}
```

### ❏ 引数<a name="arg"></a>[【top】](#top)

- 引数名はキャメルケース(先頭は`英小文字`、後続の単語の先頭は`英大文字`)で記述します。
- 引数を区切るカンマ`,`の前にはスペースを入れず、後にはスペース1文字を入れます。

**良い例**

```csharp
public void setProfile(string userId, string userName, int age) {
    // Do something
}
```

**悪い例**

```csharp
public void setProfile(string UserId,string UserName,int Age) {
    // Do something
}
```

### ❏ 配列<a name="array1"></a>[【top】](#top)

```csharp
// 宣言だけ行う場合
int[] numbers;

// 宣言と初期化を同時に行う場合
string[] seasons = new string[] {"Spring", "Summer", "Autumn", "Fall"};

// 初期化が1行の長さ制限を超える場合
string[] days = new string[] {
    "Sunday",
    "Monday",
    "Tuesday",
    "Wednesday",
    "Thrirsday",
    "Friday",
    "Saturday",
};

// 2次元配列の初期化
int[,] positionArray = new int[,] {
    {0, 0},
    {1, 2},
    {4, 3},
}

//値の参照
string monday = days[1];

// 値の代入
numbers[0] = 1;
```

- C#にはリストやキューなど、用途別のコレクションクラスが用意されているので、目的に合ったコレクションクラスを利用して下さい。

```csharp
using System.Collections.Generic;

// Listジェネリックコレクションの初期化記述例
List<string> days = new List<string>() {
    "Sunday",
    "Monday",
    "Tuesday",
    "Wednesday",
    "Thrirsday",
    "Friday",
    "Saturday",
};
```

**(参考)**
[System.Collections.Genericのコレクションクラスについて](http://msdn.microsoft.com/ja-jp/library/system.collections.generic(v=vs.90).aspx)

### ❏ 連想配列<a name="array2"></a>[【top】](#top)

- C#で連想配列を使う場合は、Dictionaryコレクションクラスを利用します。

```csharp
using System.Collections.Generic;

public enum DaysKey {
    SUNDAY,
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THIRSDAY,
    FRIDAY,
    SATURDAY,
};

Dictionary<DaysKey, string> daysName = new Dictionary<DaysKey, string>() {
    {SUNDAY, "Sunday"},
    {MONDAY, "Monday"},
    {TUESDAY, "Tuesday"},
    {WEDNESDAY, "Wednesday"},
    {THIRSDAY, "Thirsday"},
    {FRIDAY, "Friday"},
    {SATURDAY, "Saturday"},
};
```

**(参考)**
[System.Collections.Genericのコレクションクラスについて](http://msdn.microsoft.com/ja-jp/library/system.collections.generic(v=vs.90).aspx)


> ## 定数<a name="const"></a>[【top】](#top)

### ❏ ローカル/グローバル<a name="const1"></a>[【top】](#top)

- 定数名は、全て英数大文字のスネークケース(単語をアンダーバー`_`で区切る)で記述します。
- リテラルを定数として使う場合は、`const`プロパティとして定義し、`アクセス修飾子`・`const`の順にキーワードを記述します。
- オブジェクトを定数として使う場合は、`static`・`readonly`プロパティとして定義し、`アクセス修飾子`・`static`・`readonly`の順にキーワードを記述します。

**良い例**

```csharp
// リテラルの定数の場合
public const float CONSUMPTION_TAX = 0.08f;

// オブジェクトの定数の場合
private static readonly Dictionary<string, int> 
```

**悪い例**

```csharp
// リテラルの定数の場合
public const float consumptionTax = 0.08f;

// オブジェクトの定数の場合
private Dictionary<string, int> 

```

### ❏ Enum<a name="enum"></a>[【top】](#top)

- Enumの定義名は、先頭が`英大文字`のキャメルケース(各単語の先頭が`英大文字`)で記述します
- Enumの値は、全て英数大文字のスネークケース(単語をアンダーバー`_`で区切る)で記述します。

**良い例**

```csharp
public enum Days {
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THIRSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY,
}
```

**悪い例**

```csharp
public enum days {
    Monday,
    Tuesday,
    Wednesday,
    Thirsday,
    Friday,
    Saturday,
    Sunday,
}
```


> ## クラス<a name="class"></a>[【top】](#top)

### ❏ 定義<a name="class1"></a>[【top】](#top)

- クラス名は、先頭が`英大文字`のキャメルケース(各単語の先頭が`英大文字`)で記述します。
- クラス宣言にはアクセス修飾子(`public`, `protected`, `private`)を必ず記述します。
- `static`修飾子を記述する場合は、アクセス修飾子の後に記述します。
- 開き波括弧`{`は`class`の次の行の先頭に記述します。
- 閉じ波括弧`}`はクラス処理の記述の次の行の先頭に記述します。

**良い例**

```csharp
public static class StringUtility
{
}
```

**悪い例**

```csharp
static public class string_utility {
}
```

### ❏ 継承、実装<a name="class2"></a>[【top】](#top)

- 継承・実装する場合は、クラス名の直後にコロン`:`を記述し、スペースを1つ空けて、継承・実装するクラス名を列挙します。
- 継承・実装するクラス名を区切るカンマ`,`の前にはスペースを入れず、後にはスペース1文字を入れます。
- 継承・実装を同時に行う場合は、継承するクラスを先に記述します。

**良い例**

```csharp
public class StringUtility: UtilityBase, UtilityInterface, IteratorInterface
{
}
```

**悪い例**

```csharp
public class StringUtility : UtilityInterface, IteratorInterface, UtilityBase
{
}
```

### ❏ 抽象クラス<a name="class3"></a>[【top】](#top)

- 抽象クラスを定義する場合は、アクセス修飾子の後に`abstract`を記述します。

```csharp
public abstract class UtilityBase
{
}
```

### ❏ 利用<a name="class4"></a>[【top】](#top)

- 定義したクラスをインスタンス化する場合は、`new`キーワードを使ってコンストラクタを呼び出します。
- クラスに定義された定数・クラス変数にアクセスする場合は、ドット演算子`.`を使って呼び出します。

```csharp
StringUtility stringUtility = new StringUtility();
string delimiter = StringUtility.DEFAULT_DELIMITER;
```


> ## インターフェイス<a name="interface"></a>[【top】](#top)

### ❏ 定義<a name="interface1"></a>[【top】](#top)

- インターフェイスを定義する場合は、`interface`キーワードを使って記述します。
- インターフェイス名は、先頭が`英大文字`のキャメルケース(各単語の先頭が`英大文字`)で記述します。
- クラス宣言にはアクセス修飾子(`public`, `protected`, `private`)を必ず記述します。
- 開き波括弧`{`は`interface`の次の行の先頭に記述します。
- 閉じ波括弧`}`はインターフェイス宣言の次の行の先頭に記述します。

**良い例**

```csharp
public interface IteratorInterface
{
    object Current();
    void Next();
    void Reset();
}
```

**悪い例**

```csharp
interface iterator_interface {
    object Current();
    void Next();
    void Reset();
}
```


> ## プロパティ<a name="property"></a>[【top】](#top)

### ❏ 定義<a name="property1"></a>[【top】](#top)

- メンバ変数名・プロパティ名はキャメルケース(先頭は`英小文字`、後続の単語の先頭は`英大文字`)で記述します。
- プロパティを定義する場合、開き波括弧`{`はプロパティ定義・`get`・`set`と同じ行に記述します。

```csharp
public class StringUtility
{
    // メンバ変数の定義
    private string label = "LABEL";
    private string target = "";

    // プロパティの定義
    public string labeledString {
        get {
            return this.label + ":" + this.target;
        }
    }
}
```

### ❏ 抽象プロパティ<a name="property2"></a>[【top】](#top)

- 抽象プロパティを定義する場合は、アクセス修飾子の後に`abstract`を記述します。

```csharp
public abstract class CharacterBase
{
    public abstract int x {
        get;
        set;
    }
    public abstract int y {
        get;
        set;
    }
}
```

### ❏ 呼び出し<a name="property3"></a>[【top】](#top)

- クラスに定義されたメンバ変数・プロパティにアクセスする場合は、ドット演算子`.`を使って呼び出します。

```csharp
string labeledString = stringUtility.labeledString;
```


> ## メソッド<a name="method"></a>[【top】](#top)

### ❏ 定義<a name="method1"></a>[【top】](#top)

- メソッド名はキャメルケース(先頭は`英小文字`、後続の単語の先頭は`英大文字`)で記述します。
- メソッド宣言にはアクセス修飾子(`public`, `protected`, `private`)を必ず記述します。
- 開き波括弧`{`はメソッド定義と同じ行に記述します。
- 閉じ波括弧`}`はメソッド定義記述の次の行に記述します。

**良い例**

```csharp
public class StringUtility
{
    public string concatenate(string string1, string string2) {
        // Do something
    }
}
```

**悪い例**

```csharp
public class StringUtility
{
    string Concatenate(string string1, string string2)
    {
        // Do something
    }
}
```

### ❏ 抽象メソッド<a name="method2"></a>[【top】](#top)

- 抽象メソッドを定義する場合は、アクセス修飾子の後に`abstract`を記述します。

```csharp
public abstract class CharacterBase
{
    public abstract Vector getPosition();
}
```

### ❏ 呼び出し<a name="method3"></a>[【top】](#top)

- クラスに定義されたメソッドを呼び出す場合は、ドット演算子`.`を使って呼び出します。

```csharp
string name = stringUtility.concatenate(firstName, lastName);
```


> ## 関数<a name="function"></a>[【top】](#top)

### ❏ ラムダ式(無名関数/クロージャ)<a name="lambda"></a>[【top】](#top)

- ラムダ式を変数に代入して使う場合、デリゲート型を定義し、定義したデリゲート型の変数に代入します。
- ラムダ式は以下のように定義・利用します。

```csharp
public class Calculation
{
    // ラムダ式の引数・返り値の型を定義する
    delegate int Operation(int a, int b);

    public int multiply(int a, int b) {
        // ラムダ式を変数に代入する
        Operation operation = (int a, int b) => { return a * b; };
        return this.execute(operation, a, b);
    }

    private int execute(Operation operation, int a, int b) {
        return operation(a, b);
    }
}
```


> ## 名前空間<a name="namespace"></a>[【top】](#top)

### ❏ 定義<a name="namespace1"></a>[【top】](#top)

- 名前空間の名称は、先頭が`英大文字`のキャメルケース(各単語の先頭が`英大文字`)で記述します。
- 開き波括弧`{`は`namespace`の次の行の先頭に記述します。
- 閉じ波括弧`}`はクラス定義の記述の次の行の先頭に記述します。

**良い例**

```csharp
namespace Utility.Math
{
    public class Calculation
    {
    }
}
```

**悪い例**

```csharp
namespace utility.math {
    public class Calculation
    {
    }
}
```

### ❏ 利用<a name="namespace2"></a>[【top】](#top)

- 名前空間を定義しているクラスを参照する場合、ドット演算子`.`を使って参照します。
- クラス内で名前空間の指定を省略する場合、`using`ディレクティブを指定します。

```csharp
using Utility;

public class Character
{
    public void Main() {
        Math.CalculationUtility calculationUtility = new Math.CalculationUtility();
        StringUtility stringUtility = new StringUtility();
    }
}
```


> ## コメント<a name="comment"></a>[【top】](#top)

### ❏ ファイルコメント<a name="comment1"></a>[【top】](#top)

- ファイルコメントは、ファイルの先頭にコメント記述子`///`を使って記述します。
- コメント記述子`///`の後にはスペース1文字を入れます。
- ファイル内にクラスが1つしかない場合は、クラスコメントに説明を記述して、ファイルコメントを省略しても構いません。

```csharp
/// <summary>
/// 文字列ユーティリティ
/// </summary>
using Utility;

public class StringUtility
{
}
```

### ❏ クラスコメント<a name="comment2"></a>[【top】](#top)

- クラスコメントは、クラス定義の直前にコメント記述子`///`を使って記述します。
- コメント記述子`///`の後にはスペース1文字を入れます。
- クラスコメントはXML形式で、以下の要素を記述します。
 - summary:クラスの説明

**良い例**

```csharp
/// <summary>
/// 文字列ユーティリティ
/// </summary>
public class StringUtility
{
}
```

**悪い例**

```csharp
// 文字列ユーティリティ
public class StringUtility
{
}
```

### ❏ メソッドコメント<a name="comment3"></a>[【top】](#top)

- メソッドコメントは、メソッド定義の直前にコメント記述子`///`を使って記述します。
- コメント記述子`///`の後にはスペース1文字を入れます。
- メソッドコメントはXML形式で、以下の要素を記述します。
 - summary:メソッドの説明
 - returns:返り値の説明(返り値が無い場合は省略)
 - param:引数の説明(引数が無い場合は省略)

**良い例**

```csharp
public class StringUtility
{
    /// <summary>
    /// 与えられた2つの文字列を結合する
    /// </summary>
    /// <returns>結合された文字列</returns>
    /// <param name="string1">1つ目の文字列</param>
    /// <param name="string2">2つ目の文字列</param>
    public static string concatenate(string string1, string string2) {
        return string1 + string2;
    }
}
```

**悪い例**

```csharp
    // 文字列を結合する
    public static string concatenate(string string1, string string2) {
        return string1 + string2;
    }
```

### ❏ 関数コメント<a name="comment4"></a>[【top】](#top)

- C#の言語仕様に関数はありません。

### ❏ 文中コメント<a name="comment5"></a>[【top】](#top)

- 文中コメントは、コメントを付与したいステートメントの直前にコメント記述子`//`を使って記述します。
- コメント記述子`//`の後にはスペース1文字を入れます。
- 文中コメントのインデントは、コメントを付与したいステートメントのインデントに合わせます。

**良い例**

```csharp
// 2つの文字列を結合する
string resultString = string1 + string2;
```

**悪い例**

```csharp
string resultString = string1 + string2; //文字列結合
```


> ## 特殊文字列<a name="spstring"></a>[【top】](#top)

### ❏ コマンド呼び出し<a name="cmd"></a>[【top】](#top)

- C#では、`System.Diagnostics.Process.Start`メソッドを使って、外部アプリケーションを実行する事ができます。

```csharp
System.Diagnostics.Process p = System.Diagnostics.Process.Start("notepad.exe");
```


> ## ファイル<a name="file"></a>[【top】](#top)

### ❏ ファイル名<a name="filename"></a>[【top】](#top)

- ファイル名はクラス名と合わせ、拡張子を`.cs`とします。

**良い例**

- StringUtility.cs

**悪い例**

- string_utility.cs

### ❏ ファイルフォーマット<a name="format"></a>[【top】](#top)

- クラス定義内の各種定義は、以下の通りの順序で記述します。

```csharp
// 名前空間利用の定義

/// <summary>
/// サンプルクラス
/// </summary>
public class SampleClass
{
    // Enumの定義

    // 構造体の定義

    // 定数の定義
    // Public,Privateの順

    // メンバ変数・プロパティの定義
    // Public,Protected,Privateの順

    // メソッドの定義
    // Public,Protected,Privateの順
}
```
