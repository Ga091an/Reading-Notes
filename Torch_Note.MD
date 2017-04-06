# Note of Torch
> author: Guiying Li

## Basic

### Loop
- while Loop
```
while(condition)
do
   statements
end
```
- for Loop
```
for var=exp1,exp2,exp3 do  
    <执行体>  
end  
```
var从exp1变化到exp2，每次变化以exp3为步长递增var，并执行一次"执行体"。exp3是可选的，如果不指定，默认为1。
- repeat Loop
```
repeat
   statements
until( condition )
```

### 流程控制
- if 语句
```
if(布尔表达式)
then
   --[ 在布尔表达式为 true 时执行的语句 --]
end
```
- if...else 语句
```
if(布尔表达式)
then
   --[ 布尔表达式为 true 时执行该语句块 --]
else
   --[ 布尔表达式为 false 时执行该语句块 --]
end
```

### 函数
- 基本定义
```
optional_function_scope function function_name( argument1, argument2, argument3..., argumentn)
	function_body
	return result_params_comma_separated
end
```
- 可变参数
Lua函数可以接受可变数目的参数，和C语言类似在函数参数列表中使用三点（...) 表示函数有可变的参数。
Lua将函数的参数放在一个叫arg的表中，#arg 表示传入参数的个数。
```
function average(...)
   result = 0
   local arg={...}
   for i,v in ipairs(arg) do
      result = result + v
   end
   print("总共传入 " .. #arg .. " 个数")
   return result/#arg
end
```

### 运算符

#### 算术运算符
A=10， B=20

操作符 | 描述 | 实例
---|---|---
+	| 加法	| A + B 输出结果 30
- |	减法	| A - B 输出结果 -10
*	| 乘法	| A * B 输出结果 200
/	| 除法	| B / A w输出结果 2
%	| 取余	| B % A 输出结果 0
^	| 乘幂	| A^2 输出结果 100
-	| 负号	| -A 输出结果v -10

#### 关系运算符
A=10,B=20

操作符	| 描述	| 实例
---|---|----
==	| 等于，检测两个值是否相等，相等返回 true，否则返回 false	| (A == B) 为 false。
~=	| 不等于，检测两个值是否相等，相等返回 false，否则返回 true<	| (A ~= B) 为 true。
\>	| 大于，如果左边的值大于右边的值，返回 true，否则返回 false	| (A > B) 为 false。
<	| 小于，如果左边的值大于右边的值，返回 false，否则返回 true	| (A < B) 为 true。
\>=	| 大于等于，如果左边的值大于等于右边的值，返回 true，否则返回 false	| (A >= B) 返回 false。
<=	| 小于等于， 如果左边的值小于等于右边的值，返回 true，否则返回 false	| (A <= B) 返回 true。

#### 逻辑运算符
A=true, B=false

操作符	| 描述	| 实例
---|---|---
and	| 逻辑与操作符。 若 A 为 false，则返回 A，否则返回 B。	| (A and B) 为 false。
or	| 逻辑或操作符。 若 A 为 true，则返回 A，否则返回 B。	| (A or B) 为 true。
not	| 逻辑非操作符。与逻辑运算结果相反，如果条件为 true，逻辑非为 false。	| not(A and B) 为 true。

#### 其它运算符

操作符	| 描述	| 实例
---|---|---
..	| 连接两个字符串	|a..b ，其中 a 为 "Hello " ， b 为 "World", 输出结果为 "Hello World"。
\#	| 一元运算符，返回字符串或表的长度。	| #"Hello" 返回 5

#### 运算符优先级
```
优先级从高到低：
^
not    - (unary)
*      /
+      -
..
<      >      <=     >=     ~=     ==
and
or
```
除了^和..外所有的二元运算符都是左连接的。
```
a+i < b/2+1          <-->       (a+i) < ((b/2)+1)
5+x^2*8              <-->       5+((x^2)*8)
a < y and y <= z     <-->       (a < y) and (y <= z)
-x^2                 <-->       -(x^2)
x^y^z                <-->       x^(y^z)
```

### 字符串
- 单引号间的一串字符。
- 双引号间的一串字符。
- [[和]]间的一串字符。

#### 字符串操作
- string.upper(argument): 字符串全部转为大写字母。
- string.lower(argument): 字符串全部转为小写字母。
- string.gsub(mainString,findString,replaceString,num):在字符串中替换,mainString为要替换的字符串， findString 为被替换的字符，replaceString 要替换的字符，num 替换次数（可以忽略，则全部替换）。
- string.strfind (str, substr, [init, [end]]): 在一个指定的目标字符串中搜索指定的内容(第三个参数为索引),返回其具体位置。不存在则返回 nil。
- string.reverse(arg): 字符串反转。
- string.format(...)： 返回一个类似printf的格式化字符串
```
> string.format("the value is:%d",4)
the value is:4
```
- string.char(arg) 和 string.byte(arg[,int]): char 将整型数字转成字符并连接， byte 转换字符为整数值(可以指定某个字符，默认第一个字符)。
```
> string.char(97,98,99,100)
abcd
> string.byte("ABCD",4)
68
> string.byte("ABCD")
65
```
- string.len(arg): 计算字符串长度。
- string.rep(string, n)): 返回字符串string的n个拷贝
- .. : 链接两个字符串

### 数组

#### 一维数组
一维数组是最简单的数组，其逻辑结构是线性表。
```
array = {"Lua", "Tutorial"}
```
索引默认从1开始，但是因为是线性表，所以键是可以指定的。如果指定索引从0甚至负数开始，也是可以的。
```
array = {}

for i= -2, 2 do
   array[i] = i *2
end

for i = -2,2 do
   print(array[i])
end
```

#### 多维数组
多维数组即数组中包含数组或一维数组的索引键对应一个数组。
```
-- 初始化数组
array = {}
for i=1,3 do
   array[i] = {}
      for j=1,3 do
         array[i][j] = i*j
      end
end

-- 访问数组
for i=1,3 do
   for j=1,3 do
      print(array[i][j])
   end
end
```
以上的实例中，数组设定了指定的索引值，这样可以避免出现 nil 值，有利于节省内存空间。

### 迭代器

#### 泛型 for 迭代器
泛型 for 在自己内部保存迭代函数，实际上它保存三个值：迭代函数、状态常量、控制变量。
泛型 for 迭代器提供了集合的 key/value 对，语法格式如下：
```
for k, v in pairs(t) do
    print(k, v)
end
---------实例---------
array = {"Lua", "Tutorial"}

for key,value in ipairs(array)
do
   print(key, value)
end
```
以上实例中我们使用了 Lua 默认提供的迭代函数 ipairs。
下面我们看看范性for的执行过程：
- 首先，初始化，计算in后面表达式的值，表达式应该返回范性for需要的三个值：迭代函数、状态常量、控制变量；与多值赋值一样，如果表达式返回的结果个数不足三个会自动用nil补足，多出部分会被忽略。
- 第二，将状态常量和控制变量作为参数调用迭代函数（注意：对于for结构来说，状态常量没有用处，仅仅在初始化时获取他的值并传递给迭代函数）。
- 第三，将迭代函数返回的值赋给变量列表。
- 第四，如果返回的第一个值为nil循环结束，否则执行循环体。
- 第五，回到第二步再次调用迭代函数

在Lua中我们常常使用函数来描述迭代器，每次调用该函数就返回集合的下一个元素。Lua 的迭代器包含以下两种类型：
- 无状态的迭代器
- 多状态的迭代器

#### 无状态的迭代器
无状态的迭代器是指不保留任何状态的迭代器，因此在循环中我们可以利用无状态迭代器避免创建闭包花费额外的代价。
每一次迭代，迭代函数都是用两个变量（状态常量和控制变量）的值作为参数被调用，一个无状态的迭代器只利用这两个值可以获取下一个元素。
这种无状态迭代器的典型的简单的例子是ipairs，他遍历数组的每一个元素。
以下实例我们使用了一个简单的函数来实现迭代器，实现 数字 n 的平方：
```
function square(iteratorMaxCount,currentNumber)
   if currentNumber<iteratorMaxCount
   then
      currentNumber = currentNumber+1
   return currentNumber, currentNumber*currentNumber
   end
end

-- i,n = square(3,0),当square返回nil的时候停止循环
for i,n in square,3,0
do
   print(i,n)
end
```
迭代的状态包括被遍历的表（循环过程中不会改变的状态常量）和当前的索引下标（控制变量），ipairs和迭代函数都很简单，我们在Lua中可以这样实现：
```
function iter (a, i)
    i = i + 1
    local v = a[i]
    if v then
       return i, v
    end
end

function ipairs (a)
    return iter, a, 0
end
```
#### 多状态的迭代器
很多情况下，迭代器需要保存多个状态信息而不是简单的状态常量和控制变量，最简单的方法是使用闭包，还有一种方法就是将所有的状态信息封装到table内，将table作为迭代器的状态常量，因为这种情况下可以将所有的信息存放在table内，所以迭代函数通常不需要第二个参数。
```
array = {"Lua", "Tutorial"}

function elementIterator (collection)
   local index = 0
   local count = #collection
   -- 闭包函数
   return function ()
      index = index + 1
      if index <= count
      then
         --  返回迭代器的当前元素
         return collection[index]
      end
   end
end

for element in elementIterator(array)
do
   print(element)
end
```

### 表
构造器是创建和初始化表的表达式。表是Lua特有的功能强大的东西。最简单的构造函数是{}，用来创建一个空表。可以直接初始化数组:
  ```
  -- 初始化表
mytable = {}

-- 指定值
mytable[1]= "Lua"

-- 移除引用
mytable = nil
-- lua 垃圾回收会释放内存
  ```

### 模块与包
模块类似于一个封装库，从 Lua 5.1 开始，Lua 加入了标准的模块管理机制，可以把一些公用的代码放在一个文件里，以 API 接口的形式在其他地方调用，有利于代码的重用和降低代码耦合度。
Lua 的模块是由变量、函数等已知元素组成的 table，因此创建一个模块很简单，就是创建一个 table，然后把需要导出的常量、函数放入其中，最后返回这个 table 就行。以下为创建自定义模块 module.lua，文件代码格式如下：
```
-- 文件名为 module.lua
-- 定义一个名为 module 的模块
module = {}

-- 定义一个常量
module.constant = "这是一个常量"

-- 定义一个函数
function module.func1()
    io.write("这是一个公有函数！\n")
end

local function func2()
    print("这是一个私有函数！")
end

function module.func3()
    func2()
end

return module
```
由上可知，模块的结构就是一个 table 的结构，因此可以像操作调用 table 里的元素那样来操作调用模块里的常量或函数。
上面的 func2 声明为程序块的局部变量，即表示一个私有函数，因此是不能从外部访问模块里的这个私有函数，必须通过模块里的公有函数来调用.

#### require 函数
```
require("<模块名>")
require "<模块名>"
local m = require("module")
```

##### 加载机制
于自定义的模块，模块文件不是放在哪个文件目录都行，函数 require 有它自己的文件路径加载策略，它会尝试从 Lua 文件或 C 程序库中加载模块。
require 用于搜索 Lua 文件的路径是存放在全局变量 package.path 中，当 Lua 启动后，会以环境变量 LUA_PATH 的值来初始这个环境变量。如果没有找到该环境变量，则使用一个编译时定义的默认路径来初始化。
当然，如果没有 LUA_PATH 这个环境变量，也可以自定义设置，在当前用户根目录下打开 .profile 文件（没有则创建，打开 .bashrc 文件也可以），例如把 "~/lua/" 路径加入 LUA_PATH 环境变量里：
```
#LUA_PATH
export LUA_PATH="~/lua/?.lua;;"
```
文件路径以 ";" 号分隔，最后的 2 个 ";;" 表示新加的路径后面加上原来的默认路径。
接着，更新环境变量参数，使之立即生效。
如果找过目标文件，则会调用 package.loadfile 来加载模块。否则，就会去找 C 程序库。
搜索的文件路径是从全局变量 package.cpath 获取，而这个变量则是通过环境变量 LUA_CPATH 来初始。
搜索的策略跟上面的一样，只不过现在换成搜索的是 so 或 dll 类型的文件。如果找得到，那么 require 就会通过 package.loadlib 来加载它。

#### C包
<strong>这一部分，不是很懂</strong>

Lua和C是很容易结合的，使用C为Lua写包。
与Lua中写包不同，C包在使用以前必须首先加载并连接，在大多数系统中最容易的实现方式是通过动态连接库机制。
Lua在一个叫loadlib的函数内提供了所有的动态连接的功能。这个函数有两个参数:库的绝对路径和初始化函数。所以典型的调用的例子如下
```
local path = "/usr/local/lua/lib/libluasocket.so"
local f = loadlib(path, "luaopen_socket")
```
loadlib函数加载指定的库并且连接到Lua，然而它并不打开库（也就是说没有调用初始化函数），反之他返回初始化函数作为Lua的一个函数，这样我们就可以直接在Lua中调用他。

### 元表
在 Lua table 中我们可以访问对应的key来得到value值，但是却无法对两个 table 进行操作。
因此 Lua 提供了元表(Metatable)，允许我们改变table的行为，每个行为关联了对应的元方法。
例如，使用元表我们可以定义Lua如何计算两个table的相加操作a+b。
当Lua试图对两个表进行相加时，先检查两者之一是否有元表，之后检查是否有一个叫"\__add"的字段，若找到，则调用对应的值。"\__add"等即时字段，其对应的值（往往是一个函数或是table）就是"元方法"。
有两个很重要的函数来处理元表：
- setmetatable(table,metatable): 对指定table设置元表(metatable)，如果元表(metatable)中存在__metatable键值，setmetatable会失败 。
- getmetatable(table): 返回对象的元表(metatable)。

设置元表：
```
mytable = {}                          -- 普通表
mymetatable = {}                      -- 元表
setmetatable(mytable,mymetatable)     -- 把 mymetatable 设为 mytable 的元表
```
#### \__index 元方法
这是 metatable 最常用的键。
当你通过键来访问 table 的时候，如果这个键没有值，那么Lua就会寻找该table的metatable（假定有metatable）中的__index 键。如果__index包含一个表格，Lua会在表格中查找相应的键。
<strong>Remar:</strong>这相当与扩展一个表的内容。
```
> other = { foo = 3 }
> t = setmetatable({}, { __index = other })
> t.foo
3
> t.bar
nil
```
如果__index包含一个函数的话，Lua就会调用那个函数，table和键会作为参数传递给函数。
\__index 元方法查看表中元素是否存在，如果不存在，返回结果为 nil；如果存在则由 \__index 返回结果。

#### \__newindex 元方法
\__newindex 元方法用来对表更新，\__index则用来对表访问 。
当你给表的一个缺少的索引赋值，解释器就会查找\__newindex 元方法：如果存在则调用这个函数而不进行赋值操作。

#### 数学操作

模式	| 描述
--- | ---
\__add	|对应的运算符 '+'.
\__sub	|对应的运算符 '-'.
\__mul	|对应的运算符 '* '.
\__div	|对应的运算符 '/'.
\__unm	|对应的运算符 '-'.
\__concat	|对应的运算符 '..'.
\__eq	|对应的运算符 '=='.
\__lt	|对应的运算符 '<'.

#### \__call 元方法
\__call 元方法在 Lua 将表当成函数来用时被调用。

#### \__tostring 元方法
\__tostring 元方法用于修改表的输出行为。

### 协同程序
Lua 协同程序(coroutine)与线程比较类似：拥有独立的堆栈，独立的局部变量，独立的指令指针，同时又与其它协同程序共享全局变量和其它大部分东西。

线程与协同程序的主要区别在于，一个具有多个线程的程序可以同时运行几个线程，而协同程序却需要彼此协作的运行。
在任一指定时刻只有一个协同程序在运行，并且这个正在运行的协同程序只有在明确的被要求挂起的时候才会被挂起。
协同程序有点类似同步的多线程，在等待同一个线程锁的几个线程有点类似协同。

### 文件I/O
Lua I/O 库用于读取和处理文件。分为简单模式（和C一样）、完全模式。
- 简单模式（simple model）拥有一个当前输入文件和一个当前输出文件，并且提供针对这些文件相关的操作。
- 完全模式（complete model） 使用外部的文件句柄来实现。它以一种面对对象的形式，将所有的文件操作定义为文件句柄的方法

#### 基础语法
打开文件操作如下：
```
file = io.open (filename [, mode])
```
模式 |	描述
---|---
r	| 以只读方式打开文件，该文件必须存在。
w	| 打开只写文件，若文件存在则文件长度清为0，即该文件内容会消失。若文件不存在则建立该文件。
a	| 以附加的方式打开只写文件。若文件不存在，则会建立该文件，如果文件存在，写入的数据会被加到文件尾，即文件原先的内容会被保留。（EOF符保留）
r+ | 以可读写方式打开文件，该文件必须存在。
w+ |打开可读写文件，若文件存在则文件长度清为零，即该文件内容会消失。若文件不存在则建立该文件。
a+ | 与a类似，但此文件可读可写
b | 二进制模式，如果文件是二进制文件，可以加上b
+| 号表示对文件既可以读也可以写

### 错误处理
我们可以使用两个函数：assert 和 error 来处理错误。实例如下：
```
local function add(a,b)
   assert(type(a) == "number", "a 不是一个数字")
   assert(type(b) == "number", "b 不是一个数字")
   return a+b
end
add(10)
```
实例中assert首先检查第一个参数，若没问题，assert不做任何事情；否则，assert以第二个参数作为错误信息抛出。
```
error (message [, level])
```
功能：终止正在执行的函数，并返回message的内容作为错误信息(error函数永远都不会返回)
通常情况下，error会附加一些错误位置的信息到message头部。
Level参数指示获得错误的位置:
- Level=1[默认]：为调用error位置(文件+行号)
- Level=2：指出哪个调用error的函数的函数
- Level=0:不添加错误位置信息

### Debug
Lua 提供了 debug 库用于提供创建我们自定义调速器的功能。Lua 本身并未有内置的调速器，但很多开发者共享了他们的 Lua 调速器代码。

### 垃圾回收
Lua 采用了自动内存管理。 这意味着你不用操心新创建的对象需要的内存如何分配出来， 也不用考虑在对象不再被使用后怎样释放它们所占用的内存。
Lua 运行了一个垃圾收集器来收集所有死对象 （即在 Lua 中不可能再访问到的对象）来完成自动内存管理的工作。 Lua 中所有用到的内存，如：字符串、表、用户数据、函数、线程、 内部结构等，都服从自动管理。
<strong>垃圾收集器间歇率</strong>和<strong>垃圾收集器步进倍率</strong>是其中两个重要的概念。

## seq2seq-attn项目

### Remark
折腾了两三天，总算明白怎么用这个代码复现论文实验了。需要复现的论文有两篇：
1. Luong, M.T., Pham, H, D. Manning, C. Effective Approaches to Attention-based Neural Machine Translation. EMNLP,2015
2. See, A, Luong, M.T., D.Manning, C. Compression of Neural Machine Translation Models via Pruning. CoNLL, 2016.

### 论文1结果复现
首先将项目下载：https://github.com/harvardnlp/seq2seq-attn，并让其可运行，这个简单，直接安装好torch就行了。接着在项目页的最下端下载pre-trained模型。接着最重要的是：数据。
特别注意，直接从openNMT里下载wmt15数据里的newstest2013的数据，并不适合本项目，无法用这个复现出论文1和2中提到的seq2seq-attn网络的效果。要直接用项目里data下面的src-test.txt（英语）和targ-test.txt数据！！
然后，translation脚本：
```
--en to de
th evaluate.lua -model /home/deepModels/torch_models/seq2seq-attn/en-to-de-model.t7 -src_dict /home/deepModels/torch_models/seq2seq-attn/en.dict -targ_dict /home/deepModels/torch_models/seq2seq-attn/de.dict -src_file data/src-test.txt -targ_file data/targ-test.txt -output_file pred.txt -gpuid 1
--  BLEU score
perl multi-bleu.perl data/targ-test.txt < pred.txt
th evaluate.lua -model /home/deepModels/torch_models/seq2seq-attn/de-to-en-model.t7 -src_dict /home/deepModels/torch_models/seq2seq-attn/de.dict -targ_dict /home/deepModels/torch_models/seq2seq-attn/en.dict -src_file data/targ-test.txt -targ_file data/src-test.txt -output_file pred.txt -gpuid 1
--de to en
--  BLEU score
```
perl multi-bleu.perl data/src-test.txt < pred.txt
这里特别注意，multi-bleu.perl脚本要从moses项目（https://github.com/moses-smt/mosesdecoder）下载，脚本位置在scripts/generic下面。
最后可以跑出来，pretrained model中en-to-de的BLEU scroe=19.5；de-to-en的BLEU scroe=20.74。根据项目的issues页面的问题，pretrained models对应于论文1中，表格1和表格3中的“Base + reverse + dropout + global attention (location) + feed input”模型。但是，Ppl.的值依然对应不上。

### 论文2结果复现

#### luajit: not enough memory
这个问题是luajit的运行内存限制是2GB，而torch默认都是根据luajit安装的，如果要解决这个问题，就需要用原生的lua来重装torch。这个项目可以很好的解决问题：https://github.com/torch/distro。
安装好后，切换适应于不同lua的torch很容易，只要在~/.bashrc(bash用户)或是~/.zshrc(zsh用户)中将不用的torch版本注释掉就行了。一般刚安装好时，文件最下面那一行就是指定torch版本的语句。

在切换完lua后，还要安装bit module不然有些程序没法正常运行；因为luajit的bit模块是自带的，但是原生lua并不是。
```
luarocks install luabitop
```

## OpenNMT

### 安装环境
1. 只需要安装lua就行了。
2. 其次lua环境要先安装tds模块（预处理数据时发现），安装方法，使用lua自带的安装器：
   ```
     luarocks install tds
   ```
  这样运行快速入门里的例子就没问题了。
3. 注意，-gpuid 这个参数是从1开始的，如果设成0的话，会自动切换成多核cpu运行。