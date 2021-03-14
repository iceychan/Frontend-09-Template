### 使用LL算法构建AST
编译原理中字符串处理方式：使用LL算法构建AST

AST：抽象语法树

代码在计算机分析过程当中，首先就是把编程语言分词，然后把这些词构成层层嵌套的语法树的树形解构。下一步才是如何去解析执行代码。

构建语法树的过程叫做语法分析。

最著名的语法分析算法，有两种，一种是LL算法，一种是LR算法。

LL：Left Left 从左到右扫描，从左到右规约

### 四则运算的分析

- TokenNumber
  - 1 2 3 4 5 6 7 8 9 0 的组合
- Operator: +、-、*、/ 之一
- Whitespace： <SP>
- LineTerminator: <LF><CR>

加法和乘法是有优先级的关系的，需要用JavaScript的产生式去定义它的加法和乘法运算
需要把加减乘除做成一个嵌套的结构
认为加法是由左右两个乘法组成的，并且加法是可以进行连加的，所以说加法是一个重复自身的序列。
定义里会有一个递归的产生式的结构，这是在做产生式时，处理无线列表的常用手法。

把单独的数字认为是一个只有一项的乘法，把只有乘号的认为是只有一项的加法。
这样比较方便去定义一个递归的表达式。

<Expression>::=
  <AddtiveExpression><EOF>

<AdditiveExpression>::=
  <MultiplicativeExpression>
  |<AddtiveExpression><+><MultiplicativeExpression>
  |<AddtiveExpression><-><MultiplicativeExpression>

<MultiplicativeExpression>::=
  <Number>
  |<MultiplicativeExpression><*><Number>
  |<MultiplicativeExpression></><Number>

### LL语法分析
AdditiveExpression - 先把乘法展开