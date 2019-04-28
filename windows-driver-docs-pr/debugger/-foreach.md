---
title: .foreach
description: .Foreach 令牌分析一个或多个调试器命令的输出，并使用此输出中的每个值，作为一个或多个其他命令的输入。
ms.assetid: 646c86c2-a436-43d6-b0d8-32dbd423120e
keywords:
- .foreach Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .foreach
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 630844f3d36619d9f8bb03bde1bb91e93cdf8b20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336618"
---
# <a name="foreach"></a>.foreach


**.Foreach**令牌解析输出的一个或多个调试器命令和使用此输出中的每个值，作为一个或多个其他命令的输入。

```dbgcmd
.foreach [Options] ( Variable  { InCommands } ) { OutCommands } 

.foreach [Options] /s ( Variable  "InString" ) { OutCommands } 

.foreach [Options] /f ( Variable  "InFile" ) { OutCommands } 
```

## <a name="span-idddktokenforeachdbgspanspan-idddktokenforeachdbgspansyntax-elements"></a><span id="ddk_token_foreach_dbg"></span><span id="DDK_TOKEN_FOREACH_DBG"></span>语法元素


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可以是下列选项中的任意组合：

<span id="_pS_InitialSkipNumber"></span><span id="_ps_initialskipnumber"></span><span id="_PS_INITIALSKIPNUMBER"></span>**/pS** *InitialSkipNumber*  
导致要跳过的一些初始标记。 *InitialSkipNumber*指定的输出将不会传递的令牌数与指定*OutCommands*。

<span id="_ps_SkipNumber"></span><span id="_ps_skipnumber"></span><span id="_PS_SKIPNUMBER"></span>**/ps** *SkipNumber*  
会导致令牌来跳过重复每次处理一个命令。 每次令牌后将传递到指定*OutCommands*，令牌的值相等的大量*SkipNumber*将被忽略。

<span id="_______Variable______"></span><span id="_______variable______"></span><span id="_______VARIABLE______"></span> *变量*   
指定变量的名称。 此变量将用来保存在每个命令的输出*InCommands*字符串; 可以引用*变量*按名称传递给在参数中*OutCommands*. 可以使用任意字母数字字符串，尽管使用一个字符串，也可以传递为有效的十六进制数或建议不要在调试器命令。 如果该名称用于*变量*恰好与现有的全局变量、 本地变量或别名，其值将不会受到 **.foreach**命令。

<span id="_______InCommands______"></span><span id="_______incommands______"></span><span id="_______INCOMMANDS______"></span> *InCommands*   
指定一个或多个命令的输出将进行分析;生成的令牌将传递给*OutCommands*。 从输出*InCommands*不会显示。

<span id="_______InString______"></span><span id="_______instring______"></span><span id="_______INSTRING______"></span> *InString*   
用于 **/s**。 指定一个字符串，将分析;生成的令牌将传递给*OutCommands*。

<span id="_______InFile______"></span><span id="_______infile______"></span><span id="_______INFILE______"></span> *InFile*   
用于 **/f**。 指定将分析; 一个文本文件生成的令牌将传递给*OutCommands*。 文件名称*InFile*必须括在引号中。

<span id="_______OutCommands______"></span><span id="_______outcommands______"></span><span id="_______OUTCOMMANDS______"></span> *OutCommands*   
指定一个或多个命令将执行每个令牌。 每当*变量*字符串的出现它将被替换为当前的令牌。

**请注意**  时字符串*变量*将显示在*OutCommands*，它必须由空格括起来。 如果不与任何其他文本相邻-甚至是括号--它不会替换当前的令牌值，除非使用[ **$ {} （别名解释器）** ](-------alias-interpreter-.md)令牌。

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

当从输出*InCommands*，则*InString*字符串，或*InFile*文件进行分析，任意数量的空格、 制表符或回车符将被视为一个分隔符。 每个文本生成部分用于替换*变量*出现在*OutCommands*。

下面是举例 **.foreach**使用语句[ **dds** ](dds--dps--dqs--display-words-and-symbols-.md)命令在文件中找到的每个标记*myfile.txt*:

```dbgcmd
0:000> .foreach /f ( place "g:\myfile.txt") { dds place } 
```

**/PS**并 **/ps**标志可用于将仅某些令牌传递到指定*OutCommands*。 例如，以下语句将跳过中的前两个标记*myfile.txt*文件，然后将传递到第三个[ **dds**](dds--dps--dqs--display-words-and-symbols-.md)。 传递每个标记之后, 它将跳过四个标记。 结果是， **dds**将与第三、 第八、 13、 18 和 23 令牌使用和其他操作：

```dbgcmd
0:000> .foreach /pS 2 /ps 4 /f ( place "g:\myfile.txt") { dds place } 
```

有关更多示例，请使用 **.foreach**令牌，请参阅[调试器命令程序示例](debugger-command-program-examples.md)。

 

 





