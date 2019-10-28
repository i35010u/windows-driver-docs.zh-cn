---
title: 分析扩展参数
description: 分析扩展参数
ms.assetid: 3c75fb75-50d0-48e4-abf4-e4dba9a080f9
keywords:
- EngExtCpp 扩展，分析参数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e0c145b8fdd2e01b19155a4ad1727b13a68a43e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838820"
---
# <a name="parsing-extension-arguments"></a>分析扩展参数


EngExtCpp 扩展框架提供了帮助分析传递到扩展的命令行参数的方法。 若要利用这些方法，扩展必须首先在[**EXT\_command**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nf-engextcpp-ext_command)宏中声明命令行参数的格式。

若要跳过由框架完成的命令行参数分析并让扩展本身分析参数，请将命令行说明设置为 `"{{custom}}"`，并使用方法[**GetRawArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548226(v=vs.85))获取用于分析的命令行参数。

打印时，将自动包装命令行说明字符串以适应显示的列宽。 但是，可以使用 "`\n`" 将换行符嵌入到说明字符串中，以开始新行。

命令行说明可以为**NULL**或空字符串。 如果发生上述任一情况，则表示 extension 命令不采用任何参数。

### <a name="span-idcommand_line_descriptionspanspan-idcommand_line_descriptionspancommand-line-description"></a><span id="command_line_description"></span><span id="COMMAND_LINE_DESCRIPTION"></span>命令行说明

命令行参数的说明是包含两种类型的组件的序列：指令和参数。 说明可以选择包含每个指令中的一个指令，并且最多可以包含64个参数。

### <a name="span-iddirectivesspanspan-iddirectivesspandirectives"></a><span id="directives"></span><span id="DIRECTIVES"></span>Using

指令指定如何分析参数。 它们由双大括号（`'{{'` 和 `'}}'`）括起来。 每个指令可以选择在描述参数的字符串中出现零次或一次。

可用的指令如下：

<span id="custom"></span><span id="CUSTOM"></span>`custom`  
关闭扩展框架完成的分析，并允许扩展执行其自己的分析。

<span id="l_str"></span><span id="L_STR"></span>`l:str`  
重写命令行参数的默认详细说明。 扩展框架将使用*str*作为所有参数的完整说明。

<span id="opt_str"></span><span id="OPT_STR"></span>`opt:str`  
覆盖命名命令的默认前缀字符。 默认值为 `"/-"`，允许将 "`/`" 或 "`-`" 用作标识命名参数的前缀。

<span id="s_str"></span><span id="S_STR"></span>`s:str`  
重写命令行参数的默认简短说明。 扩展框架将使用*str*作为所有参数的简短说明。

下面是一些指令示例。 以下字符串由分析其自身参数的扩展命令使用。 它还提供了与 automatic **！ help** extension 命令一起使用的简短和详细说明：

```dbgcmd
{{custom}}{{s:<arg1> <arg2>}}{{l:arg1 - Argument 1\narg2 - Argument 2}}
```

下面的字符串将参数选项前缀字符更改为 "`/`" 或 "`-`"。 使用此指令时，将使用 "`+arg`" 和 "`:arg`" 而不是 "`/arg`" 和 "`-arg`" 指定参数：

```dbgcmd
{{opt:+:}}
```

### <a name="span-idargumentsspanspan-idargumentsspanarguments"></a><span id="arguments"></span><span id="ARGUMENTS"></span>形参

参数可以为以下两种类型：命名和未命名。 未命名参数为 read 按位置。 这两种类型的参数还具有一个显示名称，由 help 命令使用。

参数说明用一大括号（`'{'` 和 `'}'`）括起来。

每个参数说明都具有以下语法：

```dbgcmd
{[optname];[type[,flags]];[argname];[argdesc]}
```

其中：

<span id="optname"></span><span id="OPTNAME"></span>*optname*  
参数的名称。 这是在命令和按名称提取参数的方法中使用的名称。 此名称是可选的。 如果它存在，则该参数将成为 "命名参数";它可以出现在命令行中的任何位置，并被名称引用。 如果此参数不存在，则该参数将成为 "未命名参数";它在命令行上的位置很重要，它是由其相对于其他未命名参数的位置引用的。

<span id="type"></span><span id="TYPE"></span>*类别*  
参数的类型。 这会影响参数的分析方式和检索方法。 *类型*参数可以具有下列值之一：

<span id="b"></span><span id="B"></span>b  
布尔类型。 参数存在或不存在。 可以使用[**HasArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549721(v=vs.85))检索命名的布尔参数。

<span id="e_d__s__bits_"></span><span id="E_D__S__BITS_"></span>e\[d\]\[s\]\[位\]  
表达式类型。 参数有一个数值。 可使用[**GetArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545596(v=vs.85))检索命名表达式参数，并可使用[**GetUnnamedArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549465(v=vs.85))检索未命名表达式参数。

<span id="d"></span><span id="D"></span>2-d  
表达式仅限于参数字符串中的下一个空格字符。 如果不存在这种情况，表达式计算器将使用命令行中的字符，直到它确定到达表达式的末尾。

<span id="s"></span><span id="S"></span>些  
表达式的值已签名。 否则，表达式的值为无符号。

<span id="bits"></span><span id="BITS"></span>带宽  
参数值中的位数。 *位数*的最大值为64。

<span id="s"></span><span id="S"></span>些  
String 类型。 字符串仅限于下一个空格字符。 可以使用[**GetArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545586(v=vs.85))检索命名的字符串参数，并使用[**GetUnnamedArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549464(v=vs.85))检索未命名的字符串参数。

<span id="x"></span><span id="X"></span>x-blade  
String 类型。 参数是命令行的其余部分。 使用**GetArgStr**或**GetUnnamedArgStr**检索参数，与 s 字符串类型相同。

<span id="flags"></span><span id="FLAGS"></span>*随意*  
参数标志。 它们确定分析器将如何处理参数。 *Flags*参数可以具有下列值之一：

<span id="d_expr"></span><span id="D_EXPR"></span>d = expr  
参数的默认值。 如果命令行中不存在参数，则将参数设置为*expr*。 默认值是根据参数类型分析的字符串。

<span id="ds"></span><span id="DS"></span>ds  
默认值将不会显示在 "帮助" 提供的参数说明中。

<span id="o"></span><span id="O"></span>i/o  
参数是可选的。 这是命名参数的默认值。

<span id="r"></span><span id="R"></span>迅驰  
参数是必需的。 这是未命名参数的默认值。

<span id="argname"></span><span id="ARGNAME"></span>*argname*  
参数的显示名称。 这是由 automatic **！ help**扩展命令和自动 **/？** 或 **-？** 命令行参数。 打印命令行选项的摘要时使用。

<span id="argdesc"></span><span id="ARGDESC"></span>*argdesc*  
自变量的说明。 这是由自动 **！帮助**扩展和自动 " **/？** " 打印的说明 或 " **-？** " 命令行参数。

下面是一些参数说明示例。 以下表达式定义了一个采用单个可选表达式参数的命令。 参数必须适合32位。 如果命令行中不存在该参数，将使用0x100 的默认值。

```dbgcmd
{;e32,o,d=0x100;flags;Flags to control command}
```

下面的表达式定义带有可选的布尔值 " **/v**" 参数和必需的未命名字符串参数的命令。

```dbgcmd
{v;b;;Verbose mode}{;s;name;Name of object}
```

以下表达式定义了一个命令，该命令具有可选的命名表达式参数 **/oname** *expr*和可选的命名字符串参数 **/eol** *str*。 如果 **/eol**存在，则将其值设置为命令行的其余部分，并且不会分析其他参数。

```dbgcmd
{oname;e;expr;Address of object}{eol;x;str;Commands to use}
```

### <a name="span-idcommand_linespanspan-idcommand_linespancommand-line"></a><span id="command_line"></span><span id="COMMAND_LINE"></span>命令行

以下是在命令行上分析参数的一些方法列表：

-   命名表达式和字符串参数的值在命令行上的名称之后。 例如， **/name** *expr*或 **/name** *str*。

-   对于命名的布尔参数，如果名称出现在命令行上，则该值为 true;否则为 false。

-   可在命令行中将多个单字符命名的布尔选项组合在一起。 例如，可以使用简写法 "/abc" 来编写 "/a/b/c" （除非已经有一个名为 "abc" 的参数）。

-   如果命令行包含命名参数 "？"-例如 "/？" 和 "-？" -参数分析结束，并显示扩展的帮助文本。

### <a name="span-idparsing_internalsspanspan-idparsing_internalsspanparsing-internals"></a><span id="parsing_internals"></span><span id="PARSING_INTERNALS"></span>分析内部

参数分析器使用几种方法来设置参数。

方法[**SetUnnamedArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556876(v=vs.85))将更改未命名参数的值。 而且，为方便起见， [**SetUnnamedArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556878(v=vs.85))和[**SetUnnamedArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556879(v=vs.85))方法将分别设置未命名字符串和表达式参数。

命名参数存在类似的方法。 [**SetArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556614(v=vs.85))用于更改任何命名参数的值， [**SetArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556618(v=vs.85))和[**SetArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556622(v=vs.85))分别用于命名字符串和表达式参数。

 

 





