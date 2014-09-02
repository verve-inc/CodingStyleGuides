#VERVEコーディング規約雛形

> ## 概要

本文書は、VERVEでのコーディング規約を定めるものである。

> ## 整形

### ❏ インデント

**規約**

スペース4つを使用する。

**理由**

タブを使用すると、エディタの設定によってインデントの深さが変わって見えるため。

### ❏ 文字コード

**規約**

UTF-8を使用する。

**理由**

主要なOSで認識することができるため。

### ❏ 改行コード

**規約**

LFを使用する。

**理由**

Linuxシステム上で稼働するサービスが多いため。

### ❏ 1行の長さ

**規約**

1行100文字を超えないように、複数行に分割する。 100文字を超える場合は、適度に改行を入れる。

**理由**

多くのコーディング規約では80文字以内と定めているが、最近のディスプレイでは80文字はかえって短すぎるため。

**例**

```java
String longText =
    "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"
    + "bbbbbbbbbbbbbbbbbbbbbbbb";
```
> ## リテラル

### ❏ 数値 ※言語仕様

```java
int i = 1; // 10進数
int j = 0x0a; // 16進数
```

### ❏ 文字列

char型はシングルクォート、String型はダブルクォートでくくる。 ※言語仕様

**例**

```java
char c = 'a';
String s = "bbb";
```

**規約**

文字および文字列をnew してはならない。

**理由**

文字および文字列をnew すると、同じ値であっても毎回新しいインスタンスが生成されることになり、
プログラムの実行速度やメモリの使用量に悪影響を及ぼす。
以下の"良い例"に示す方法で文字および文字列を宣言することで同じ値を複数の変数の間で共有するなど、
JVMによってコードが最適化される可能性が高くなる。

**良い例**
```java
String title = "Hamlet";
char initial = 'H';
```

**悪い例**
```java
String title = new String("Hamlet");
char initial = new Character('H');
```

### ❏ 論理値

真はtrue、偽はfalseと記述する（小文字で記述する）。 ※言語仕様

**例**

```java
boolean t = true;
boolean f = false;
```

**規約**

論理値をnew してはならない。

**理由**

規約「文字および文字列をnew してはならない。」と同様。

**良い例**

```java
boolean t = true;
boolean f = false;
```

**悪い例**

```java
boolean t = new Boolean(true);
boolean f = new Boolean(false);
```

### ❏ 未定義値 ※言語仕様

小文字で'null'と書く。

**例**

```java
String s = null;
```

### ❏ ヒアドキュメント

言語仕様に無い。

> ## 演算子

### ❏ 算術演算子

**規約1**

"+"、"-"、"*"、"/"、"%"の前後にはスペース１文字を入れる

**理由**

見やすいため。

**良い例**

```java
i = 0;
```

**悪い例**

```java
i=0;
```

**規約2**

インクリメント"++"、デクリメント"--"と操作する変数の間には空白を入れない。

**理由**

演算子と変数の間が空いていると、操作対象の変数がどれなのか判別しにくいため。

**良い例**

```java
++i, j--
```

**悪い例**

```java
++ i, j --
```

### ❏ 文字列結合演算子

**規約1**

演算子の前後にはスペース１文字を入れる。

**理由**

見やすいため。

**良い例**

```java
String longText = "あいうえお" + "かきくけこ";
```

**悪い例**

```java
String longText = "あいうえお"+"かきくけこ";
```

**規約2**

折り返す場合は"+"の前に改行を入れ、２行目以降はインデントを１つ下げる。

**理由**

2行目以降が、1行目の続きであることが分かりやすいため。

**例**

```java
String longText = "あいうえお"
    + "かきくけこ"
    + "さしすせそ";
```

### ❏ 比較演算子

**規約1**

比較演算子は変数を左に、定数を右に置く。

**理由**

変数と定数の順序を統一することで、可読性を高めるため。

**良い例**

```java
if (i == 5)
```

**悪い例**

```java
if (5 == i)
```

**規約2**

比較演算子の前後には、スペース１文字を入れる。

**理由**

見やすいため。

**良い例**

```java
if (i == j)
```

**悪い例**

```java
if (i==j)
```

### ❏ 論理演算子

**規約**

論理演算子の前後には、スペース１文字を入れる。

**理由**

見やすいため。

**良い例**

```java
return r && s;
```

**悪い例**

```java
return r&&s;
```

### ❏ ビット演算子

**規約1**

AND("&")、OR("|")、XOR("^")、シフト("<<", ">>")の前後には、スペース１文字を入れる。

**理由**

見やすいため。

**良い例**

```java
i = i & 0x11;
```

**悪い例**

```java
i = i&0x11;
```

**規約2**

NOT("~")と操作する変数の間には、空白を入れない。

**理由**

NOT演算子がどの変数にかかっているかを明確にするため。

**良い例**

```java
i = ~i;
```

**悪い例**

```java
i = ~ i;
```

### ❏ 代入演算子

**規約**

代入演算子の前後には、スペース１文字を入れる。

**理由**

見やすいため。

**良い例**

```java
i = 1;
i += 1;
```

**悪い例**

```java
i=1;
i+=1;
```

### ❏ 三項演算子

使用することはOK。

**規約1**

演算子の前後には、スペース１文字を入れる。

**理由**

見やすいため。

**良い例**

```java
text = i > 0 ? "0より大きい" : "0以下";
```

**悪い例**

```java
text = i > 0?"0より大きい":"0以下";
```

**規約2**

途中で行を折り返す場合は演算子の前に改行を入れ、２行目以降はインデントを１つ下げる。
#### 例:
```java
longText = i > 0
    ? "0よりは大きいと思います"
    : "0以下のはずです"
```

> ## 制御構文

### ❏ 条件式

**規約1**

開き丸括弧"("の前と閉じ丸括弧")"の後にはスペース１文字を入れる。

**理由**

メソッドの括弧と区別をつけるため。

**良い例**

```java
if (i == 0) {
}
```

**悪い例**

```java
if(i == 0){
}
```

**規約2**

開き丸括弧"("の後と閉じ丸括弧")"の前には、スペースを空けない。

**理由**

行が冗長になるのを避けるため。

**良い例**

```java
if (i == 0) {
}
```

**悪い例**

```java
if ( i == 0 ) {
}
```

**規約3**

開き波括弧"{"は条件式と同じ行に記述する。

閉じ波括弧"}"の前で改行を入れ、インデントの深さは条件式と揃える。

**理由**

見やすいため。

**良い例**

```java
if (i == 0) {
}
```

**悪い例1**

```java
if (i == 0)
{
}
```

**悪い例2**

```java
if (i == 0) {
    }
```

**規約4**

文法上、波括弧を省略できる場合でも、波括弧を省略してはならない。

**理由**

波括弧を省略すると、どこからどこまでがif文の中身なのかが分かりにくくなるため。

**良い例**

```java
if (i == 0) {
    text = "0です。";
}
```

**悪い例**

```java
if (i == 0)
    text = "0です。";
```

**規約5**

制御構文のネストは、最大3つまでとする。
制御構文のネストが4つ以上になる場合は、メソッドを分割するなどして対応する。

**理由**

複雑なコードはバグが発生しやすく、加えて可読性・保守性が損なわれるため。

**悪い例**

※一見して、何をしているのかわかりにくい。

```java
public List<Map<String, Object>> getShoppingCart(HttpServletRequest request) {

    List<Map<String, Object>> shoppingCart = getRequestedGoodsList(request);
    if (shoppingCart != null) {
        for (Map<String, Object> goods : shoppingCart) {
            if ((Boolean) goods.get("isInCampaign") == true) {
                Double discountRate = (Double) goods.get("discountRate");
                if (discountRate != null) {
                    if (discountRate > 1.0) {
                        throw new IllegalStateException("割引率が1を超えています。");
                    }
                    goods.put("price", (int) ((Integer) goods.get("price") * (1 - discountRate)));
                }
            }
        }
    }
    return shoppingCart;
}
```

**良い例**

※ネストされた処理をメソッドとして切り出し、さらにフローを整理したことで、先ほどより見やすくなった。

```java
public List<Map<String, Object>> getShoppingCart(HttpServletRequest) {

    List<Map<String, Object>> shoppingCart = getRequestedGoodsList(request);
    if (shoppingCart == null) {
            return null;
    }
    
    for (Map<String, Object> goods : shoppingCart) {
        if ((Boolean) goods.get("isInCampaign") == true) {
            goods.put("price", calculateCampaignPrice(goods));
        }
    }
    return shoppingCart;
}

private static int calculateCampaignPrice(Map<String, Object> goods) {

    Double discountRate = (Double) goods.get("discountRate");
    if (discountRate == null) {
        return (Integer) goods.get("price");
    }
    
    if (discountRate > 1.0) {
        throw new IllegalStateException("割引率が1を超えています。");
    }
    return (int) ((Integer) goods.get("price") * (1 - discountRate));
}
```

### ❏ if文

**規約1**

else句、else if句は、閉じ波括弧"}"の後にスペース１文字を空けて記述する。

**理由**

ソースファイルが冗長になるのを防ぐため。

**良い例**

```java
if (i == 0) {
    s = "iは0です。";
} else {
    s = "iは0以外です。";
}
```

**悪い例1**

```java
if (i == 0) {
    s = "iは0です。";
}else{
    s = "iは0以外です。";
}
```

**悪い例2**

```java
if (i == 0) {
    s = "iは0です。";
}
else {
    s = "iは0以外です。";
}
```

**規約2**

空のブロックを記述してはならない。

**理由**

ソースコードが冗長になる上、可読性が損なわれるため。

**良い例**

```Java
if (i == 0) {
    s = "iは0です。";
}
```

**悪い例**

```Java
if (i == 0) {
    s = "iは0です。";
} else {

}
```

### ❏ for文

**規約1**

条件式に記述するセミコロン";"の前にはスペースを入れず、後にはスペース１文字を入れる。

**良い例**

```java
for (int i = 0; i < ary.length; i++) {
    s += ary[i];
}
```

**悪い例**

```java
for (int i = 0 ; i < ary.length ; i++) {
    s += ary[i];
}
```

**規約2**

拡張for文が使用可能な場合は、拡張for文を使用する。

**理由**

不要な変数の宣言をなくし、コードの可読性を高めるため。

**良い例**

```java
for (String element : ary) {
    text += element + "<br>";
}
```

**悪い例**

```java
for (int i = 0; i < ary.length; i++) {
    text += ary[i] + "<br>";
}
```

### ❏ while文

※while分の書き方については、条件式の規約と同じ。

**規約** do-while文の書き方
開き波括弧"{"はdo句と同じ行に記述し、do句との間にスペース1文字を入れる。
while句は閉じ波括弧"}"と同じ行に記述し、閉じ波括弧との間にスペース1文字を入れる。

**理由**

見やすいため。

**良い例**

```java
do {
    s += i;
} while (i < n);
```

**悪い例**

```java
do
{
    s += i;
}
while (i < n);
```

### ❏ foreach文

※Javaでは拡張for文について説明する。

**規約**

条件式に記述するコロン":"の前後には、スペース１文字を入れる。

**理由**

見やすいため。

**良い例**

```java
for (String element : ary) {
    s += element + "<br>";
}
```

**悪い例**

```java
for (String element:ary) {
    s += element + "<br>";
}
```

### ❏ switch文

**規約1**

case句はswitch句より１つインデントを下げる。

case句の中身の処理文は、case句より１つインデントを下げる。

**理由**

見やすいため。

**良い例**

```java
switch (i) {
    case 0:
        text = "0です。";
        break;
    }
```

**悪い例**

```java
switch (i) {
case 0:
text = "0です。";
break;
}
```

**規約2**

意図的にbreak句を省略する場合は、コメントで"// No break"を記述しておく。

**理由**

何も書かれていないと、後から読んだ人は本当に必要ないのか書き忘れなのか判断をつけにくいため。

**良い例**

```java
switch (i) {
    case 0:
        text = "0です。";
        // No break
    case 1:
        text += "1です。";
        break;
    }
```

**規約3**

default句は省略しない。

default句で何も処理する必要がない場合は、コメントで"// Do nothing"と記述しておく。

**理由**

default句が省略されていたり、中身に何も書かれていないと、
後から読んだ人は本当に必要ないのか書き忘れなのか判断をつけにくいため。

**良い例**

```java
switch (i) {
    case 0:
        text = "0です。";
        break;
    default:
        // Do nothing
}
```

**規約4**

一番下に記述するcase句も、"break"を省略しない。

**理由**

後にcase句が追加された時に、"break"の書き忘れによってバグが発生するのを防ぐため。

**良い例**

```java
switch (i) {
    case 0:
        text = "0です。";
        break;
    case 1:
        text = "1です。";
        break;
    default:
        // Do nothing
}
```

**悪い例**

```java
switch (i) {
    case 0:
        text = "0です。";
        break;
    case 1:
        text = "1です。";
    default:
        // Do nothing
}
```

**規約5**

default句はcase句の下に記述する。

**理由**

Javaの仕様上、default句はどの位置に記述しても一番最後に評価されるが、誤読を防ぐために一番下に記述する。

**良い例**

```java
switch (i) {
    case 0:
        text = "0です。";
        break;
    default:
        text = "0以外です。";
    }
```

**悪い例**

```java
switch (i) {
    default:
        text = "0以外です。";
    case 0:
        text = "0です。";
        break;
}
```

### ❏ try/catch文

**規約1**

try句と開き波括弧”{”の間には、スペース1文字を入れる。<br>
try句の閉じ波括弧"}"とcatch句の間は改行せず、同じ行にスペース1文字を入れて記述する。

**理由**

改行の数が増えすぎると見づらいため。

**良い例**

```java
try {
    int i = Integer.parseInt(s);
} catch (Exception e) {
    System.out.println(e);
}
```

**悪い例**

```java
try
{
    int i = Integer.parseInt(s);
}
catch (Exception e)
{
    System.out.println(e);
}
```

**規約2**

catch句と開き括弧"("の間にはスペース1文字を入れる。<br>
catch句の開き括弧"("の後ろと閉じ括弧")"の前には、スペースを空けない。<br>
catch句の閉じ括弧"("と開き波括弧"{"の間には、スペース1文字を入れる。

**理由**

見やすいため

**良い例**

```java
try {
    int i = Integer.parseInt(s);
} catch (Exception e) {
    System.out.println(e);
}
```

**悪い例**

```java
try {
    int i = Integer.parseInt(s);
} catch( Exception e ){
    System.out.println(e);
}
```

**規約3**

try句で開いたリソースは、finally句の中でクローズする。

**理由**

例外が発生した場合でも、確実にクローズ処理を実行するため。

**良い例**

```java
Connection conn;
try {
    conn = DriverManager.getConnection(URI_OF_DATABASE);
    // 中略
} catch (SQLException e) {
    // 例外処理
} finally {
    if (conn != null) {
        try { conn.close(); }
        catch (SQLException ex) { /* Do nothing */ }
    }
}
```

**悪い例**

```java
Connection conn;
try {
    conn = DriverManager.getConnection(URL_OF_DATABASE);
    // 中略  ※ここで例外が発生すると、クローズ処理が実行されない
    conn.close();
} catch (SQLException e) {
    // 例外処理
}
```

**規約4**

finally句から例外を投げてはいけない。

**理由**

finally句の中で例外が発生すると、try句内で発生した例外を隠ぺいしてしまうため。

**良い例**

```java
Connection conn;
try {
    conn = DriverManager.getConnection(URI_OF_DATABASE);
    conn.query(SQL);  // ここで例外が発生!
} catch (SQLException e) {
    // 例外処理
} finally {
    if (conn != null) {
        try { conn.close(); }  // finally句内で発生した例外は、外部に伝搬させない
        catch (SQLException ex) { /* Do nothing */ }
    }
}
```

**悪い例**

finally句内で変数connのnullチェックをしていない。<br>
そのため、try句の1行目で例外が発生した場合、このコードブロックの呼び出し元には
finally句で発生したNullPointerExceptionが伝搬することになり、本来の例外発生の原因が分からなくなってしまう。
```java
Connection conn;
try {
    conn = DriverManager.getConnection(URI_OF_DATABASE);  // ここで例外が発生
    conn.query(SQL);
} catch (SQLException e) {
    // 例外処理
} finally {
    conn.close();  // ここでNullPointerExceptionが発生
}
```

> ## 変数

### ❏ ローカル変数

**規約1**

変数名は、頭文字が小文字のキャメルケースとする。

**理由**

OracleのJava言語コーディング規約に則るため。

**良い例**

```java
String firstName;
```

**悪い例**

```java
String FirstName;
String firstname;
```

**規約2**

ローマ字英語を使用しない。

**理由**

格好悪いため。

**良い例**

```java
boolean hasMarried;
```

**悪い例**

```java
boolean hasKikon;
```

**規約3**

英単語は省略しない。

**理由**

他人が読んで意図を理解しやすいコードにするため。

**良い例**

```java
String familyName;
```
####悪い例 :
```java
String fName;
```
※ただし、省略形が一般に普及している単語は例外とする。
  例： URL, HTTP, API, PC,  …

**規約4**

boolean変数は、true/falseの意味が分かるように命名する。

**理由**

他人が読んで意図を理解しやすいコードにするため。

**良い例**

```java
boolean isMale;
```

**悪い例**

```java
boolean sex;  // trueの場合がどちらで、falseの場合がどちらなのかが分からない。
```

### ❏ グローバル変数

※Javaではstatic変数が他の言語のグローバル変数に相当するが、規約はローカル変数と同様であるため割愛する。

### ❏ 引数

※ローカル変数の規約と同様であるため割愛する。

### ❏ 配列

**規約1**

配列は「型名[] 変数名」の形式で宣言する。

**理由**

「型名 変数名[]」形式の宣言方法はC言語の名残で残っている（らしい）が、Java言語本来の言語仕様ではないため。

**良い例**

```java
String[] addressList = new String[5];
```

**悪い例**

```java
String addressList[] = new String[5];
```

**規約2**

配列を宣言する際、型名と開き角括弧"["および閉じ角括弧"]"の間にはスペースを空けない。

**理由**

見やすいため。

**良い例**

```java
String[] addressList = new String[5];
```

**悪い例**

```java
String [ ] addressList = new String[5];
```

**規約3**

配列を初期化する際、開き角括弧"["と閉じ角括弧"]"の前後にはスペースを空けない。

**理由**

見やすいため。

**良い例**

```java
String[] addressList = new String[5];
```

**悪い例**

```java
String[] addressList = new String [ 5 ];
```

**規約4**

配列の初期化時に値を代入する際、
開き波括弧"{"は変数名と同じ行にスペース1文字を空けて記述する。
閉じ波括弧"}"の前で改行を入れ、インデントの深さは変数名と揃える。
開き波括弧と閉じ波括弧の間の行は、インデントを一つ下げる。

**理由**

見やすいため。

**良い例**

```java
String[] addressList = new String[] {
    "渋谷区渋谷",
    "新宿区歌舞伎町",
    "北区池袋"
};
```

**悪い例**

```java
String[] addressList = new String[]
    {
    "渋谷区渋谷",
    "新宿区歌舞伎町",
    "北区池袋"};
```

### ❏ 連想配列

※言語仕様に無い。

> ## 定数

### ❏ ローカル/グローバル

**規約1**

ローカル定数は使用しない。
すべてstatic定数として定義する。

**理由**

ローカル定数を宣言した場合、生成したインスタンスの数だけその定数が初期化されるため。

**良い例**

```java
public static final double PI = 3.14;
```

**悪い例**

```java
public final double PI = 3.14;
```

**規約2**

変数名はすべて大文字で宣言し、複数の単語で構成する場合はアンダーバー"_"で区切る。

**理由**

定数であることを明示するため。

**良い例**

```java
public static final String FAMILY_NAME = "田中";
```

**悪い例1**

```java
public static final String familyName = "田中";
```

**悪い例2 **

```java
public static final String FAMILYNAME = "田中";
```

### ❏ enum

**規約1**

クラス名は、頭文字が大文字のキャメルケースとする。

**理由**

クラス名であることを明示するため。

**良い例**

```java
enum PrimeNumber {
    // 省略
}
```

**悪い例**

```java
enum prime_number {
    // 省略
}
```

**規約2**

要素名はすべて大文字で宣言し、複数の単語で構成する場合はアンダーバー"_"で区切る。

**理由**

enumの要素は不変であるため、定数と同じ形式で記述する。

**良い例**

```java
enum CatType {
    AMERICAN_SHORT_HAIR, // アメリカンショートヘアー
    SIAMESE_CAT, // シャム猫
    MIKE_CAT // 三毛猫
}
```

**悪い例**

```java
enum CatType {
    americanShortHair, // アメリカンショートヘアー
    siameseCat, // シャム猫
    mikeCat // 三毛猫
}
```

> ## クラス

### ❏ 定義

**規約1**

クラス名は、先頭が英大文字のキャメルケースとする。

**良い例**

```java
public class SomethingClass {
}
```

**悪い例**

```java
public class something_class {
}
```

**規約2**

ローマ字英語を使用しない。

**理由**

格好悪いため。

**良い例**

```java
public class Advertisement {
}
```

**悪い例**

```java
public class Koukoku {
}
```

**規約3**

英単語は省略しない。

**理由**

他人が読んで意図を理解しやすいコードにするため。

**良い例**

```java
public class ClickAdvertisement {
}
```
####悪い例 :
```java
public class CAdv {
}
```
※ただし、省略形が一般に普及している単語は例外とする。
  例： URL, HTTP, API, PC,  …

**規約4**

開き波括弧"{"は、クラス名を宣言する行と同じ行に、半角スペース1文字を空けて記述する。
閉じ波括弧"}"は、独立した行にクラス名を宣言した行と同じインデントで記述する。

**良い例**

```java
public class SomethingClass {
}
```

**悪い例**

```java
public class SomethingClass
{
    }
```

**規約5**

インスタンス化する必要のないクラスは、インスタンス化できないように作成する。

**理由**

定数クラスおよびユーティリティクラスなど、インスタンス化する必要のないクラスを作成することがある。
しかし、そのようなクラスがインスタンス化可能なように作成されているとそのクラスの用途が不明確になり、
間違った方法で使用されたり、変更されたりしてしまうため。

**例**

※インスタンス化できないクラスの作成方法

```java
public class UtilityClass {

    /**
     * 引数なしのプライベートコンストラクタを定義し、デフォルトコンストラクタの生成を防ぐ。
     */
    private UtilityClass() {
        /*
         * さらにこのコンストラクタを呼び出すとAssertionErrorをスローし、
         * 絶対にインスタンスの生成ができないようにしている。
         */
        throw new AssertionError();
    }
    
    public static void function1() {
        ...
    }
    
    ...
}
```

### ❏ 継承、実装

**規約1**

クラスを継承する場合は、クラス名の後に半角スペース1文字を空けて"extends 【クラス名】"と記述する。

**良い例**

```java
public class ChildClass extends ParentClass {
}
```

**悪い例**

```java
public class ChildClass  extends  ParentClass {
}
```

**規約2**

インターフェースを実装する場合は、クラス名の後に半角スペース1文字を空けて"inplements 【インターフェース名】"と記述する。
複数のインターフェースを実装する場合、インターフェース名を区切るカンマ","の前にはスペースを空けず、カンマの後ろに半角スペース1つを空ける。

**良い例**

```java
public class SomethingClass implements Interface1, Interface2 {
}
```

**悪い例**

```java
public class SomethingClass implements Interface1 , Interace2 {
}
```

**規約3**

クラスの継承とインターフェースの実装を同時に宣言する場合は、"extends"句を先に記述する。（※言語仕様）

**例**

```java
public class SomethingClass extends ParentClass implements Interface1 {
}
```

**規約4**

クラスを宣言する行が長くなりすぎる場合、クラス名の宣言の後に改げ用を入れ、2行目のインデントを1つ下げる。

**例**

```java
public class SomethingClass
    extends ParentClass implements Interface1, Interface2 {
}
```

### ❏ 抽象クラス

**規約**

抽象クラスを宣言する場合、アクセス修飾子の後に"abstract"キーワードを宣言する。

**良い例**

```java
public abstract class AbstractClass {
}
```

**悪い例**

```java
abstract public class AbstractClass {
}
```

### ❏ 利用

**規約**

クラスをインスタンス化する場合、newキーワードを使ってコンストラクタを呼び出す。（※言語仕様）

**例**

```java
SomethingClass some = new SomethingClass();
```

**規約**

クラスに定義されて定数・クラス変数にアクセスする際は、ドット演算子"."を使用する。

**例**

```java
String someVariable = SomethingClass.someVariable;
```

> ## インターフェイス

### ❏ 定義

**規約1**

インターフェイスを定義する場合は、interfaceキーワードを使って記述する。（※言語仕様）

**例**

```java
/**
 * Iteratorインターフェイスの再生産
 */
public interface MyIterator {
    public boolean hasNext();
    public Object next();
    public void remove();
}
```

**規約2**

インターフェイス名は、クラス名に準ずる。

**良い例**

```java
public interface MyIterator {
    ...省略
}
```

**悪い例**

```java
public interface my_iterator {
    ...省略
}
```

**規約3**

能力付加型のインターフェイスは、名前の末尾に"able"をつける。<br>
能力付加型のインターフェイスとは、そのインターフェイスを実装したクラスに対して
ある能力を付加する役割を持つもののことである。

**理由**

Javaコーディングスタイルガイドに準拠するため。

**例**

```java
public interface Readable{
    ...省略
}
```

> ## プロパティ

※Javaでは、メンバフィールド、スタティックフィールドについて説明する。
  
### ❏ 定義

**規約1**

メンバフィールド名、スタティックフィールド名は、先頭が英小文字のキャメルケースとする。

**理由**

記述方法を統一することで、コードを読みやすくするため。

**良い例**

```java
private static int accessCounter = 0;
private String pageName = null;
```

**悪い例**

```java
private static int access_counter = 0;
private String PageName = null;
```

**規約2**

修飾子を記述する順番は、下記のとおりとする。

```
  1. public
  2. protected
  3. private
  4. static
  5. final
  6. transient
  7. volatile
```

**理由**

記述する順序を統一することで、コードを読みやすくするため。<br>
なお、この記述順序はJava言語仕様で指定されている推奨修飾子順序に準拠している。

**良い例**

```java
public static final int MAX_VALUE = 10;
private volatile int counter = 0;
```

**悪い例**

```java
final static public int MAX_VALUE = 10;
volatile private int counter = 0;
```

### ❏ 呼び出し

**規約1**

メンバフィールド、スタティックフィールドにアクセスする場合は、ドット演算子"."を使用する。※言語仕様

**例**

```java
String familyName = person.familyName;

int maxValue = HtmlPage.MAX_VALUE;
```

**規約2**

スタティックフィールドにアクセスする際、オブジェクト名や"this"演算子を用いてアクセスしてはならない。

**理由**

メンバフィールドと混同しやすく、可読性が低下するため。

**良い例**

```java
// クラス内部からアクセスする場合
public class GoodExample {
    public static final int MAX_VALUE = 10;
    
    public void sampleMethod() {
        int maxValue = MAX_VALUE;
    }
}

// クラス外部からアクセスする場合
public class OtherClass {
    public void sampleMethod() {
        GoodExample object = new GoodExample();
        int maxValue = GoodExample.MAX_VALUE;
    }
}
```

**悪い例**

```java
// クラス内部からアクセスする場合
public class BadExample {
    public static final int MAX_VALUE = 10;
    
    public void sampleMethod() {
        int maxValue = this.MAX_VALUE;
    }
}

// クラス外部からアクセスする場合
public class OtherClass {
    public void sampleMethod() {
        BadExample object = new BadExample();
        int maxValue = object.MAX_VALUE;
    }
}
```

> ## メソッド

### ❏ 定義

**規約1**

メソッド名は頭文字が小文字のキャメルケースで定義する。

**理由**

OracleのJava言語コーディング規約に則るため。

**よい例**

```java
public void doSomething() {
    ...
}
```

**悪い例**

```java
public void do_something() {
    ...
}
```

**規約2**

開き波括弧`{`はメソッド定義と同じ行に、半角スペース１つを空けて記述する。

**理由**

書式を統一することで、他人が読みやすいコードにするため。

**よい例**

```java
public void doSomething() {
    ...
}
```

**悪い例**

```java
public void doSomething(){
    ...
}

public void doSomething2()
{
    ...
}
```

**規約3**

メソッド名の英単語は省略しない。

**理由**

他人が読んで理解しやすいコードにするため。

**よい例**

```java
public String getFirstName() {
    ...
}
```

**悪い例**

```java
public String getFName() {
    ...
}
```

※ただし、省略形が一般に普及している単語は例外とする。
　　例: URL, HTTP, API, PC, …

**規約4**

１つのメソッドの行数は、空白行・コメント行も含めて30行以下とする。

**理由**

それ以上長くなると、そのメソッドが何をしているのかを理解することが難しくなるため。
また、長過ぎるメソッドは本来複数のメソッドに分割できる複数の役割を負っていることが多い。

### ❏ 抽象メソッド

**規約**

抽象メソッドを定義する場合は、アクセス修飾子の後に`abstract`を記述する。（※言語仕様）

> ## 関数

※言語仕様にない。

> ## 名前空間

※Javaコーディング規約では、パッケージ名について記述する。

### ❏ 定義

パッケージ名を定義する場合は、クラスファイルの１行目に以下のように記述する。（※言語仕様）

```Java
package {パッケージ名};
```

### ❏ 利用

異なるパッケージに定義されている型にアクセスする場合、ドット演算子`.`を使用する。（※言語仕様）

```Java
public class SampleClass {

    public void doSomething() {

        Object[] obj = new Object[] {"b", "c", "a"};
        java.util.Arrays.sort(obj);

        System.out.println(java.util.Arrays.toString(obj));  // [a, b, c] と表示される
    }
}
```

クラスファイル内でパッケージ名の指定を省略する場合、`import`ディレクティブを使用する。（※言語仕様）

```Java
import java.util.Arrays;

public class SampleClass {

    public void doSomething() {

        Object[] obj = new Object[] {"b", "c", "a"};
        Arrays.sort(obj);

        System.out.println(Arrays.toString(obj));  // [a, b, c] と表示される
    }
}
```

クラスファイル内で異なるパッケージの型に定義されたstaticメソッドを型名を省略して使用する場合、
`import static`ディレクティブを使用する。（※言語仕様）

```Java

import static java.util.Arrays.sort;

import java.util.Arrays;

public class SampleClass {

    public void doSomething() {

        Object[] obj = new Object[] {"b", "c", "a"};
        sort(obj);

        System.out.println(Arrays.toString(obj));  // [a, b, c] と表示される
    }
}
```

**規約**

import文およびimport static文に、ワイルドカードを使用してはならない。

**理由**

ワイルドカードを使用して型またはメソッドをインポートすると、意図していない型やメソッドを
使用してしまう可能性があるため。

**良い例**

※使用する方だけをインポートしている。

```Java
import java.util.List;
import java.util.ArrayList;
```

**悪い例**

※使用していない型も、全てインポートしてしまう。

```Java
import java.util.*;
```

**Tips**

Eclipseで開発している場合、以下のショートカットキーで自動的にインポート文を成形できる。
　Windows : `alt` + `shift` + `o`
　Mac : `command` + `shift` + `o`

> ## コメント

### ❏ ファイルコメント

**規約**

ファイルコメントは、ファイルの先頭にコメント記述子`/*  */`を使って記述する。

**例**

```java
/*
 * サンプルコメント。
 */
package jp.ne.sample;

public class SampleClass {
    … 中略
}
```

### ❏ クラスコメント

**規約1**

クラスコメントは、クラスの宣言の直前にコメント記述子`/** */`を使って記述する。

**例**

```java
package jp.ne.sample;

/**
 * サンプルクラス。
 */
public class SampleClass {
    … 中略
}
```

### ❏ メソッドコメント

**規約1**

メソッドコメントは、メソッドの宣言の直前にコメント記述子`/** */`を使って記述する。

**例**

```java
/**
 * サンプルメソッド。
 */
public void doSomething() {
    … 中略
}
```

**規約2**

メソッドコメントには、原則以下を記述する。

```java
/**
 * 一行目にメソッドの概要、必須。
 * ２行目以降にメソッドの詳細。getter、setterのように詳細を記述するまでもないものについては、省略可能。
 * 
 * @params param1 引数の説明。引数がないメソッドは不要。
 * @params ...
 * @return 戻り値の説明。戻り値がないメソッドは不要。
 * @throws [例外の型名1] 何をしたら/何が起きたらこの例外が発生するかを説明する。
 *     throws句を記述する必要のないRuntimeException についても記述する。
 *     例外を投げないメソッドは不要
 * @throws [例外の型名2] ...
 */
public String doSomething(int param1, int ...) throws Exception {
    ...（中略）
}
```

**良い例**

```java
/**
 * 引数name が、猫の品種であるかどうかを判定する。
 * 判定基準は、ウィキペディアの「http://ja.wikipedia.org/wiki/猫の品種の一覧」をもとにしている。
 * 
 * @params name 猫の品種。カタカナの半角・全角は区別しないが、ひらがなや漢字が混ざると間違った結果を返す場合がある。
 * @return 引数nameが猫の品種である場合、true。
 * @throws NullPointerException 引数nameがnullの場合。
 */
public boolean isCatBreedsName(String name) {
    ...（中略）
}
```

**悪い例**

※説明が不十分であったり、そもそも書かれていなかったりするため、この説明文だけではメソッドの使い方が分からない。

```java
/**
 * 引数nameが、猫の品種であるかどうかを判定する。
 * 
 * @params name 猫の品種。
 * @return 
 */
public boolean isCatBreedsName(String name) {
    ...（中略）
}
```

### ❏ 関数コメント

### ❏ 文中コメント

> ## 特殊文字列

### ❏ コマンド呼び出し

> ## ファイル

### ❏ ファイル名
