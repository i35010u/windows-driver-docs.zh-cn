---
title: 分析扩展参数
description: 分析扩展参数
ms.assetid: 3c75fb75-50d0-48e4-abf4-e4dba9a080f9
keywords:
- EngExtCpp 扩展，分析参数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbb5f3c32c17eb7bb84485c9c44943ac6a02966f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338728"
---
# <a name="parsing-extension-arguments"></a>分析扩展参数


EngExtCpp 扩展框架提供方法以帮助分析传递到扩展的命令行参数。 若要充分利用这些方法，该扩展必须首先声明中的命令行参数的格式[ **EXT\_命令**](https://msdn.microsoft.com/library/windows/hardware/ff544514)宏。

绕过命令行参数分析由框架完成，并允许扩展本身将这些参数分析、 将命令行描述设置为`"{{custom}}"`，并使用方法[ **GetRawArgStr** ](https://msdn.microsoft.com/library/windows/hardware/ff548226)若要获取用于分析的命令行参数。

打印，以适合显示的列宽度时，将自动包装命令行说明字符串。 但是，在说明字符串-使用中嵌入换行字符`\n`-若要开始新行。

命令行说明可以是**NULL**或空字符串。 如果任何一个发生，它指示扩展命令不接受任何参数。

### <a name="span-idcommandlinedescriptionspanspan-idcommandlinedescriptionspancommand-line-description"></a><span id="command_line_description"></span><span id="COMMAND_LINE_DESCRIPTION"></span>命令行说明

命令行参数的说明是一个序列，其中包含两种类型的组件： 指令和自变量。 描述可以选择包含每个指令之一，并且可以包含最多 64 个参数。

### <a name="span-iddirectivesspanspan-iddirectivesspandirectives"></a><span id="directives"></span><span id="DIRECTIVES"></span>指令

指令指定分析参数的方式。 它们括在双大括号 (`'{{'`和`'}}'`)。 每个指令还可以选择显示零或一次在字符串中的描述的参数。

提供了以下指令：

<span id="custom"></span><span id="CUSTOM"></span>`custom`  
关闭由扩展框架完成的分析，并允许执行其自己的分析的扩展。

<span id="l_str"></span><span id="L_STR"></span>`l:str`  
重写的命令行参数的默认长说明。 将使用扩展框架*str*为所有参数的完整说明。

<span id="opt_str"></span><span id="OPT_STR"></span>`opt:str`  
重写默认前缀字符的命名命令。 默认值是`"/-"`，允许 '`/`或`-`便可用作标识的前缀命名参数。

<span id="s_str"></span><span id="S_STR"></span>`s:str`  
重写的命令行参数的默认简短描述。 将使用扩展框架*str*为所有参数的简短描述。

下面是一些示例的指令。 使用以下字符串分析自己的自变量是扩展命令。 它还介绍了短期和长期使用与自动 **！ 帮助**扩展命令：

```dbgcmd
{{custom}}{{s:<arg1> <arg2>}}{{l:arg1 - Argument 1\narg2 - Argument 2}}
```

以下字符串更改为的参数选项的前缀字符`/`或`-`。 包含此指令，参数将使用指定 '`+arg`'和'`:arg`而不是 of`/arg`和`-arg`:

```dbgcmd
{{opt:+:}}
```

### <a name="span-idargumentsspanspan-idargumentsspanarguments"></a><span id="arguments"></span><span id="ARGUMENTS"></span>自变量

参数可以是两种类型： 名为和未命名。 按位置读取未命名的参数。 这两种类型的参数还具有使用帮助命令的显示名称。

参数说明括在单个大括号 (`'{'`和`'}'`)。

每个自变量说明具有以下语法：

```dbgcmd
{[optname];[type[,flags]];[argname];[argdesc]}
```

其中：

<span id="optname"></span><span id="OPTNAME"></span>*optname*  
参数的名称。 这是用于命令和提取自变量的方法中按名称的名称。 此名称是可选的。 如果存在，该参数将成为"已命名的参数;"它可以在命令行上出现任何位置，并按名称引用。 如果不存在，该参数将变为"未命名的参数;"在命令行上的其位置很重要，并由其位置相对于其他未命名参数来引用它。

<span id="type"></span><span id="TYPE"></span>*type*  
自变量的类型。 这会影响如何分析参数并检索方式。 *类型*参数可以具有下列值之一：

<span id="b"></span><span id="B"></span>b  
布尔值类型。 该参数是存在或不存在。 可以使用检索命名的布尔参数[ **HasArg**](https://msdn.microsoft.com/library/windows/hardware/ff549721)。

<span id="e_d__s__bits_"></span><span id="E_D__S__BITS_"></span>e\[d\]\[s\]\[bits\]  
表达式类型。 自变量具有数字值。 可以使用检索命名的表达式参数[ **GetArgU64** ](https://msdn.microsoft.com/library/windows/hardware/ff545596) ，可以使用检索未命名的表达式自变量[ **GetUnnamedArgU64** ](https://msdn.microsoft.com/library/windows/hardware/ff549465).

<span id="d"></span><span id="D"></span>d  
该表达式仅限于参数字符串中下一步的空格字符。 如果不存在，表达式计算器将使用命令行中的字符，直到它会确定它已达到表达式的末尾。

<span id="s"></span><span id="S"></span>s  
表达式的值进行签名。 否则，该表达式的值进行签名。

<span id="bits"></span><span id="BITS"></span>bits  
自变量的值中的位数。 最大值*bits*为 64。

<span id="s"></span><span id="S"></span>s  
字符串类型。 字符串被限制为下一步的空格字符。 可以使用检索命名的字符串自变量[ **GetArgStr** ](https://msdn.microsoft.com/library/windows/hardware/ff545586) ，可以使用检索未命名的字符串自变量[ **GetUnnamedArgStr** ](https://msdn.microsoft.com/library/windows/hardware/ff549464).

<span id="x"></span><span id="X"></span>x  
字符串类型。 该参数是命令行的其余部分。 使用检索参数**GetArgStr**或**GetUnnamedArgStr**，如同处理 s 字符串类型。

<span id="flags"></span><span id="FLAGS"></span>*flags*  
参数的标志。 这些属性决定分析器将如何处理自变量。 *标志*参数可以具有下列值之一：

<span id="d_expr"></span><span id="D_EXPR"></span>d=expr  
参数的默认值。 如果该参数不存在，命令行，则参数设置为*expr*。 默认值为一个字符串，根据自变量的类型解析。

<span id="ds"></span><span id="DS"></span>ds  
将不会提供帮助的参数说明中显示的默认值。

<span id="o"></span><span id="O"></span>o  
该参数可选。 这是命名参数的默认值。

<span id="r"></span><span id="R"></span>r  
参数是必需的。 这是未命名参数的默认值。

<span id="argname"></span><span id="ARGNAME"></span>*argname*  
自变量的显示名称。 这是自动使用的名称 **！ 帮助**扩展插件命令并通过自动 **/？** 或 **-？** 命令行参数。 打印命令行选项的摘要时使用。

<span id="argdesc"></span><span id="ARGDESC"></span>*argdesc*  
参数的说明。 这是由自动打印的描述 **！ 帮助**扩展和由自动"**/？**" or "**-?**" 命令行参数。

下面是一些示例的参数说明。 下面的表达式定义采用一个可选表达式参数的命令。 自变量必须容纳在 32 位。 如果参数不是命令行上存在，将使用 0x100 的默认值。

```dbgcmd
{;e32,o,d=0x100;flags;Flags to control command}
```

下面的表达式定义了一个命令使用可选的布尔值"**/v**"参数和必需的未命名的字符串自变量。

```dbgcmd
{v;b;;Verbose mode}{;s;name;Name of object}
```

下面的表达式定义了具有一个可选的命名表达式参数的命令 **/oname** *expr*和一个可选的命名字符串自变量 **/eol** *str*。 如果 **/eol**存在，则其值将设置为命令行的其余部分，将分析任何进一步的自变量。

```dbgcmd
{oname;e;expr;Address of object}{eol;x;str;Commands to use}
```

### <a name="span-idcommandlinespanspan-idcommandlinespancommand-line"></a><span id="command_line"></span><span id="COMMAND_LINE"></span>命令行

下面是一组命令行上将解析参数的一些方法：

-   命名的表达式和字符串自变量的值按照在命令行上的名称。 例如， **/name** *expr*或 **/名称** *str*。

-   命名的布尔参数的值为 true，如果名称出现在命令行;false 否则为。

-   多个单字符名的布尔选项可以在命令行上组合在一起。 例如，"/a /b /c"可以编写使用速记表示法"/ abc"（除非已存在名为"abc"的参数）。

-   如果命令行中包含的命名的参数"？"-例如，"/？" 和"-？" -显示参数分析结束，并且该扩展的帮助文本。

### <a name="span-idparsinginternalsspanspan-idparsinginternalsspanparsing-internals"></a><span id="parsing_internals"></span><span id="PARSING_INTERNALS"></span>分析内部机制

参数分析器使用的几种方法用于设置参数。

该方法[ **SetUnnamedArg** ](https://msdn.microsoft.com/library/windows/hardware/ff556876)将未命名参数的值更改。 并为方便起见，方法[ **SetUnnamedArgStr** ](https://msdn.microsoft.com/library/windows/hardware/ff556878)并[ **SetUnnamedArgU64** ](https://msdn.microsoft.com/library/windows/hardware/ff556879)将设置未命名的字符串和表达式参数分别。

命名参数的存在类似的方法。 [**SetArg** ](https://msdn.microsoft.com/library/windows/hardware/ff556614)用于更改任何命名自变量的值和[ **SetArgStr** ](https://msdn.microsoft.com/library/windows/hardware/ff556618)并[ **SetArgU64** ](https://msdn.microsoft.com/library/windows/hardware/ff556622)命名的字符串和表达式参数分别用于。

 

 





