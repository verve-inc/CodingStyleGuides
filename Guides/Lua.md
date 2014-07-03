# VERVEコーディング規約(Lua)<a name="top"></a>


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
`スペース４つ`を使用します。
　  
　  
### ❏ 文字コード<a name="code"></a>[【top】](#top)
`UTF-8`を使用します。
　  
　  
### ❏ 改行コード<a name="newline"></a>[【top】](#top)
`LF`を使用します。
　  
　  
### ❏ 1行の長さ<a name="length"></a>[【top】](#top)
ソフトリミットは`120文字`を上限とし、実際`80文字`以内に記述します。 
　  
　  
　  
　  
　  

> ## リテラル<a name="literal"></a>[【top】](#top)

### ❏ 数値<a name="int"></a>[【top】](#top)

整数

```lua
local a = 1234 -- 10進整数
local a = -123 -- 負の数
local a = 0x1a -- 16進数 (10進数の26と等価)
```

浮動小数点数

```lua
local a = 1.234 
local b = 1.2e3 
local c = 7e-10
```

拡張

```lua
a = tonumber(11)       --- a = 11
a = tonumber("11")     --- a = 11
a = tonumber("11", 2)  --- a = 3
a = tonumber("11", 16) --- a = 17
a = tonumber("0x11")   --- a = 17

```
　  
　  
### ❏ 文字列<a name="string"></a>[【top】](#top)

- Lua の文字列は、一重引用符`(' ')`または、二重引用符`(" ")`で囲まれる文字の系列です。  
文字列中では、以下のエスケープシーケンスを用いることができます。

```lua
\n  -- 改行
\t  -- 水平タブ
\r  -- 復帰
\v  -- 垂直タブ
\xxx  -- 文字コードが 10 進数 xxx の文字
\a  -- ベル
\b  -- 一文字後退
\f  -- フォームフィード
\\  -- バックスラッシュ
\"  -- 二重引用符 (")
\'  -- 一重引用符 (')
\\  -- バックスラッシュ(\)
```

- 二重引用符で囲まれた文字列中では、一重引用符をエスケープ無しでそのまま用いることができます。  
しかし、ある文字列を囲むのに用いられている引用符合をその文字列中で用いるときには、  
エスケープする必要があります。  
次の二つは文字列として有効であり、同一の文字列です。

```lua
s = "Olho d'agua"
s = 'Olho d\'agua'
```

- 二重の角括弧も文字列を囲むのに用いられます。  
二重引用符や一重引用符と異なり、この中ではエスケープシーケンスが解釈されません。  
また、それが入れ子になる場合は、角括弧の間に=を入れて、`[=[　]=]`のように明示します。   

```lua
s = [[ This is a text
that crosses
a string more than and contains one
string nested: [=[nested]=] in the end!]]
```
　  
　  
### ❏ 論理値<a name="boolen"></a>[【top】](#top)

全て小文字で表記します。

**良い例**

```lua
true
false
```

**悪い例**

```lua
TRUE
FALSE
```
　  
　  
### ❏ 未定義値<a name="nil"></a>[【top】](#top)
全て小文字で表記します。

```lua
nill
```
　  
　  
### ❏ ヒアドキュメント<a name="doc"></a>[【top】](#top)
下記のように記述します。

```lua
s = [[複数行文字列も
このように
代入可能]]

print(s)
```
　  
　  
　  
　  
　  

> ## 演算子<a name="operator"></a>[【top】](#top)

### ❏ 算術演算子<a name="operator1"></a>[【top】](#top)

```lua
 +     -- 加算
 -     -- 減算
 *     -- 乗算
 /     -- 除算
 %     -- 剰余
```
　  
　  
### ❏ 文字列結合演算子<a name="operator2"></a>[【top】](#top)

```lua
local a = "abc"
lcoal str = a .. "def" -- abcdef
```
　  
　  
### ❏ 比較演算子<a name="operator3"></a>[【top】](#top)

```lua
<     -- 小さい
>     -- 大きい
<=    -- 小さいか等しい
>=    -- 大きいか等しい
==    -- 等しい
~=    -- 異なる
```
　  
　  
### ❏ 論理演算子<a name="operator4"></a>[【top】](#top)

```lua
and        -- かつ
or         -- または
not        -- でない
```
　  
　  
### ❏ ビット演算子<a name="operator5"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
### ❏ 代入演算子<a name="operator6"></a>[【top】](#top)

演算子の前後にはスペースを1文字入れる。

```lua
str = hoge .. "hoge"
```
　  
　  
### ❏ 三項演算子<a name="operator7"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
　  
　  
　  
　  
> ##  制御構文<a name="structure"></a>[【top】](#top)

### ❏ 条件式<a name="condition"></a>[【top】](#top)

- 制御構造キーワードの後には、1スペースを設けなければなりません。
- 構造本文は、条件式から開業して1インデント下げなければなりません。
- 2つ以上の条件式は、改行して記述して下さい。

**良い例**

```lua
if hoge then
    return
end
```
```lua

if x == 1 and y == 1 then
    return
end
```
```lua
if x == 1 and
    y == 2 or 
    y == 1 then
    return
end
```

**悪い例**

```lua
if hoge then return end
```

```lua
if x == 1
    and y == 1 then
    return
end
```
　  
　  
### ❏ if文<a name="if"></a>[【top】](#top)

条件式を囲う括弧は、入れません。

```lua
if hoge then
    -- test    
elseif hogehoge then
    -- logic
else
    -- logic 
end
```
　  
　  
### ❏ for文<a name="for"></a>[【top】](#top)

条件式を囲う括弧は、入れません。

```lua
for i=1,10 do
    -- logic 
end
```
```lua
for i=1, n do
    -- logic
end
```
　  
　  
### ❏ while文<a name="while"></a>[【top】](#top)

条件式を囲う括弧は、入れません。

```lua
i = 1
while i <= 10 do
    print ( i .. "回目:Hello world!" )
    i = i + 1
end
```
　  
　  
### ❏ foreach文<a name="foreach"></a>[【top】](#top)

```lua
for i,v in ipairs(table_name) do
    -- logic
end

for k,v in pairs(table_name) do
    -- logic
end
```
　  
　  
### ❏ switch文<a name="switch"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
### try/catch文<a name="exeption"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
　  
　  
　  
> ## 変数<a name="variable"></a>[【top】](#top)

### ❏ ローカル変数<a name="localvar"></a>[【top】](#top)

**命名規則**

- 先頭は英字でなければなりません。
- 予約語は使用できません。
- 数字を安易に使用してはいけません。
- 小文字で開始する`camelCaps方式`を使用しなければなりません。
- `k`や`v`のような変数が許されるのは、小さなループ内で使用する場合のみです。

**使用規則**

- 頭にかならず`local`をつけて下さい。
- 変数定義の際に`=`の前後はスペースを入れなければなりません。
- 1ファイルにつきローカル変数の上限は200個までなので、  
定数の用に使用する場合でローカル変数を複数作成する場合は、  
下記のように記述して下さい。

**良い例**

```lua
hogeHoge = ''
```
```lua
local hogeType = {
    hogeTypeOff = 0
    hogeTypeOn = 1
}
print(hogeType.hogeTypeOn)
```

**悪い例**

```lua
HOGE_HOGE = ''
hoge_hoge = ''
HogeHoge = ''
```
```lua
local hogeTypeOff = 0
local hogeTypeOn = 1 
print(hogeTypeOn)
```
　  
　  
### ❏ グローバル変数<a name="globalvar"></a>[【top】](#top)

**命名規則**

- 先頭は英字でなければなりません。
- 予約語は使用できません。
- 数字を安易に使用してはいけません。
- 大文字で開始する`パスカル記法`を使用しなければなりません。
- `k`や`v`のような変数が許されるのは、小さなループ内で使用する場合のみです。

**使用規則**

- 変数定義の際に`=`の前後はスペースを入れなければなりません。

**良い例**

```lua
HogeHoge = ''
```

**悪い例**

```lua
hogeHoge = ''
hoge_hoge = ''
HOGE_HOGE = ''
```
　  
　  
### ❏ 引数<a name="arg"></a>[【top】](#top)

[ローカル変数](#localvar)と同様の規則です。
　  
　  
### ❏ 配列<a name="array1"></a>[【top】](#top)

**使用規則**

- 初期化を必ず行って下さい。
- 配列に要素を指定する場合、文字列であれば改行しインデントして下さい。
- 配列に要素を指定する場合、数値であれば一行で記述して構いません。
- カンマの後は、スペースを入れて下さい。
- 最後の要素までカンマをつけて下さい。

```lua
local tbl = {}

local tbl = {
    "func", 
    "hoge",
}
```

```lua
local tbl = {
    {0, 0, 0, 0},
    {0, 0, 0, 0},
}
```
　  
　  
### ❏ 連想配列<a name="array2"></a>[【top】](#top)

**使用規則**

- 初期化を必ず行って下さい。
- 配列に要素を指定する場合、必ず改行しインデントして下さい。
- 最後の要素までカンマをつけて下さい。

```lua
local tbl = {}

local tbl = {
    func = func, 
    hoge = hoge,
}
```
　  
　  
　  
　  
　  
　  
> ## 定数<a name="const"></a>[【top】](#top)

### ❏ ローカル/グローバル<a name="const1"></a>[【top】](#top)

- luaには定数はありませんので、変数を代替として使用します。
- 全て大文字の`_`区切りで、記述して下さい。
- また、定数として変数を利用する場合は、必ずコメントを書いて下さい。

**良い例**

```lua
HOGE_TYPE = 1    -- hoge1
```

**悪い例**

```lua
HogeType = 1
hoge_type = 1
```
　  
　  
### ❏ enum<a name="enum"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
　  
　  
　  
　  
> ## クラス<a name="class"></a>[【top】](#top)

### ❏ 定義<a name="class1"></a>[【top】](#top)

- `new`で定義して下さい。

```lua
-- effect.lua
function new(params)
end
```
　  
　  
### ❏ 継承、実装<a name="class2"></a>[【top】](#top)

- `__index `で継承します。

```lua
-- inheri.lua
-- 基本となる Animal クラスを定義
Animal = {}
Animal.name = "unknown"
Animal.showProfile = function(self)
			print("*** profile")
			print("name="..self.name)
		     end

-- Animal を継承して Dog クラスを作る
Dog = {}
Dog.new = function(name)
	     local obj = {}
	     obj.name = name
	     setmetatable(obj, {__index=Animal})
	     return obj
	  end

-- インスタンスを生成する
ff = Dog.new("FeiFei")
ff:showProfile()
```
　  
　  
### ❏ 抽象クラス<a name="class3"></a>[【top】](#top)

- 定義・継承・実装と同様です。
　  
　
　  

### ❏ 利用<a name="class4"></a>[【top】](#top)

- 最後の要素までカンマをつけて下さい。

```lua
local Effect = require 'effect'
EffectObj = Effect.new({
        param1 = 1,
        param2 = 2,
    })

```
　  
　  
　  
　  
　  
　  
> ## インターフェイス<a name="interface"></a>[【top】](#top)

### ❏ 定義<a name="interface1"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
　  
　  
　  
> ## プロパティ<a name="property"></a>[【top】](#top)

### ❏ 定義<a name="property1"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
### ❏ 抽象プロパティ<a name="property2"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
### ❏ 呼び出し<a name="property3"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
　  
　  
　  
　  
> ## メソッド<a name="method"></a>[【top】](#top)

### ❏ 定義<a name="method1"></a>[【top】](#top)

- 半角英数字のみ使用可能です。
- 数字は安易に使用してはいけません。
- 小文字で開始する`camelCaps方式`で記述して下さい。
- `self`をつけて定義して下さい。

```lua
-- effect.lua
function new(params)
    function self.play()
        -- Logic
    end
end
```
　  
　  
### ❏ 抽象メソッド<a name="method2"></a>[【top】](#top)

- 定義と同様です。
　  
　  
　  

### ❏ 呼び出し<a name="method3"></a>[【top】](#top)

- クラスに定義されたメソッドを呼び出す場合は、ドット演算子.を使って呼び出します。

```lua
local Effect = require 'effect'
EffectObj = Effect.new({
        param1 = 1,
        param2 = 2,
    })

EffectObj.play()
```
　  
　  
　  
　  
　  
　  
> ## 関数<a name="function"></a>[【top】](#top)

### ❏ ローカル<a name="function1"></a>[【top】](#top)

- 半角英数字のみ使用可能です。
- 数字は安易に使用してはいけません。
- 小文字で開始する`camelCaps方式`で記述して下さい。

**良い例**

```lua
local function hogeHoge
    -- logic
end
```

**良い例**

```lua
local function hoge_hoge1
    -- logic
end

local function hoge_hoge2
    -- logic
end
```
　  
　  
### ❏ グローバル<a name="function2"></a>[【top】](#top)

- 半角英数字のみ使用可能です。
- 数字は安易に使用してはいけません。
- 大文字で開始する`パスカル方式`で記述して下さい。

**良い例**

```lua
local function HogeHoge
    -- logic
end
```

**良い例**

```lua
local function hogeHoge1
    -- logic
end

local function hogeHoge2
    -- logic
end
```
　  
　  
### ❏ ラムダ式(無名関数/クロージャ)<a name="lambda"></a>[【top】](#top)

```lua
function()
```
　  
　  
　  
　  
　  
　  
> ## 名前空間<a name="namespace"></a>[【top】](#top)

### ❏ 定義<a name="namespace1"></a>[【top】](#top)

**命名規則**

- 半角英数字のみ使用可能です。
- 数字は安易に使用してはいけません。
- 大文字から開始する、`パスカル記法`で書いて下さい。

**使用例**

- アプリケーション全体で参照が必要な場合のみ使用して下さい。
- 必ず`main.lua`で定義して下さい。


```lua
_G.UserData = {}
```
　  
　  
### ❏ 利用<a name="namespace2"></a>[【top】](#top)

```lua
print(_G.UserData)
```
　  
　  
　  
　  
　  
　  
> ## コメント<a name="comment"></a>[【top】](#top)

### ❏ ファイルコメント<a name="comment1"></a>[【top】](#top)

- ファイルの先頭に記述して下さい。
- `--[[]]--`のコメント方式を採用します。
- 下記のように記述して下さい。

```lua
--[[
  model manager
]]--
```
　  
　  
### ❏ クラスコメント<a name="comment2"></a>[【top】](#top)

クラスは、luaの言語仕様にありません。
　  
　  
### ❏ メソッドコメント<a name="comment3"></a>[【top】](#top)

- メソッド定義の前に記述して下さい。
- `--[[]]--`のコメント方式を採用します。
- 下記のように記述して下さい。

```lua
--[[
  hogeを取得する
  param1 int ID 
  param2 string 取得するhogeの名前
]]--
function getHoge(param1, param2)
    -- logic
end
```
　  
　  
### ❏ 関数コメント<a name="comment4"></a>[【top】](#top)

- 関数定義の前に記述して下さい。
- `--[[]]--`のコメント方式を採用します。
- 下記のように記述して下さい。

```lua
--[[
  hogeを取得する
  param1 int ID 
  param2 string 取得するhogeの名前
]]--
function getHoge(param1, param2)
    -- logic
end
```
　  
　  
### ❏ 文中コメント<a name="comment5"></a>[【top】](#top)

- 処理のひとかたまりに対して、端的にコメントして下さい。
- 何を意図しているか、わかるコメントを心がけて下さい。
- 開発中以外、todoを記載するのは禁止します。
- `if~elseif~else`に対するコメントは、条件式の後の処理中に記載して下さい。
- 一行コメントの場合は、`--`を使用して下さい。
- 複数行のコメントの場合は`--[[ ]]--`を使用して下さい。
- 一行コメントの場合は、--の後にスペースを入れて下さい。
- 複数行コメントの場合は、改行して使用して下さい。
- インデントは、実装箇所と揃えて記述して下さい。

```lua
-- 短いコメント
```
```lua
--[[
    複数行にわたるコメント
]]--
```
```lua
if hoge == 1 then
    -- comment1
    print('hello world1')
else
    -- comment2
    print('hello world2')
end
```
　  
　  
　  
　  
　  
　  
> ## 特殊文字列<a name="spstring"></a>[【top】](#top)


### ❏ コマンド呼び出し<a name="cmd"></a>[【top】](#top)

luaの言語仕様にありません。
　  
　  
　  
　  
　  
　  
> ## ファイル<a name="file"></a>[【top】](#top)

### ❏ ファイル名<a name="filename"></a>[【top】](#top)

- 小文字の`_`区切りで作成して下さい。
- 半角英数字のみ使用可能です。
- 数字は安易に使用しないで下さい。
- フレームワークに指定がある場合は、そちらを優先して下さい。
- ディレクトリと同じキーワードは入れないでください。

**良い例**

```lua
help_manager.lua

eff/pixi_dust.lua
eff/slide.lua
```

**悪い例**

```lua
helpManager.lua

eff/eff_pixi_dust.lua
eff/eff_slide.lua
```
　  
　  
### ❏ ファイルフォーマット<a name="format"></a>[【top】](#top)

```lua
--[[
    flurry 共通クラス
]]--

module(..., package.seeall)

local analytics = require "analytics"

--[[
    Const
]]-----------------------------------------------------------------------------

local APPLICATION_CODE = 'BV4DQJRR8P3WNSRS78ZK'


--[[
    Local variable
]]-----------------------------------------------------------------------------

local initFlag = false

--[[
    Global variable
]]-----------------------------------------------------------------------------

IintFlag = false

--[[
    Local  function
]]-----------------------------------------------------------------------------

--[[
    初期化
]]--
local function init(type)
    -- logic
end


--[[
    Global function
]]-----------------------------------------------------------------------------

--[[
    @param eventName string
    @param param table 属性
]]--
function SendEvent(eventName, param)
    -- logic
end

```

