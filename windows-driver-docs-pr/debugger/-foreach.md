---
title: .foreach
description: Foreach 标记分析一个或多个调试器命令的输出，并使用此输出中的每个值作为一个或多个附加命令的输入。
keywords:
- foreach Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .foreach
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d580a892b22b82e64421fec3fdbc93a3e57733e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822643"
---
# <a name="foreach"></a>.foreach


**Foreach** 标记分析一个或多个调试器命令的输出，并使用此输出中的每个值作为一个或多个附加命令的输入。

```dbgcmd
.foreach [Options] ( Variable  { InCommands } ) { OutCommands } 

.foreach [Options] /s ( Variable  "InString" ) { OutCommands } 

.foreach [Options] /f ( Variable  "InFile" ) { OutCommands } 
```

## <a name="span-idddk_token_foreach_dbgspanspan-idddk_token_foreach_dbgspansyntax-elements"></a><span id="ddk_token_foreach_dbg"></span><span id="DDK_TOKEN_FOREACH_DBG"></span>语法元素


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可以是下列选项的任意组合：

<span id="_pS_InitialSkipNumber"></span><span id="_ps_initialskipnumber"></span><span id="_PS_INITIALSKIPNUMBER"></span>**/PS** *InitialSkipNumber*  
导致跳过某些初始标记。 *InitialSkipNumber* 指定将不传递到指定 *OutCommands* 的输出令牌的数目。

<span id="_ps_SkipNumber"></span><span id="_ps_skipnumber"></span><span id="_PS_SKIPNUMBER"></span>**/Ps** *SkipNumber*  
导致每次处理命令时重复跳过标记。 每次将令牌传递到指定的 *OutCommands* 后，将忽略多个等于 *SkipNumber* 值的令牌。

<span id="_______Variable______"></span><span id="_______variable______"></span><span id="_______VARIABLE______"></span>*变量*   
指定变量名称。 此变量将用于保存 *InCommands* 字符串中每个命令的输出;可以在传递给 *OutCommands* 的参数中按名称引用 *变量*。 可以使用任何字母数字字符串，但不建议使用也可以传递给有效十六进制数或调试器命令的字符串。 如果用于 *变量* 的名称与现有全局变量、局部变量或别名相匹配，则 **foreach** 命令不会影响其值。

<span id="_______InCommands______"></span><span id="_______incommands______"></span><span id="_______INCOMMANDS______"></span>*InCommands*   
指定一个或多个将分析其输出的命令;生成的令牌将传递给 *OutCommands*。 不显示 *InCommands* 的输出。

<span id="_______InString______"></span><span id="_______instring______"></span><span id="_______INSTRING______"></span>*InString*   
与 **/s** 一起使用。 指定一个要分析的字符串;生成的令牌将传递给 *OutCommands*。

<span id="_______InFile______"></span><span id="_______infile______"></span><span id="_______INFILE______"></span>*InFile*   
与 **/f** 一起使用。 指定将进行分析的文本文件;生成的令牌将传递给 *OutCommands*。 文件名 *InFile* 必须用引号引起来。

<span id="_______OutCommands______"></span><span id="_______outcommands______"></span><span id="_______OUTCOMMANDS______"></span>*OutCommands*   
指定将对每个标记执行的一个或多个命令。 只要 *变量* 字符串发生，就会被当前标记替换。

**注意**   当字符串 *变量* 出现在 *OutCommands* 中时，它必须由空格括起来。 如果它与任何其他文本（甚至是括号）相邻，则不会将其替换为当前标记值，除非你使用 [**$ {} (别名解释器)**](-------alias-interpreter-.md) 令牌。

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

分析来自 *InCommands*、 *InString* 字符串或 *InFile* 文件的输出时，任意数量的空格、制表符或回车符将被视为单个分隔符。 每个生成的文本段都用来替换 *OutCommands* 中显示的 *变量*。

下面是在文件 *myfile.txt* 中找到的每个标记上使用 [**dds**](dds--dps--dqs--display-words-and-symbols-.md)命令的 **foreach** 语句的示例：

```dbgcmd
0:000> .foreach /f ( place "g:\myfile.txt") { dds place } 
```

**/PS** 和 **/pS** 标志可用于仅将特定标记传递到指定的 *OutCommands*。 例如，下面的语句将跳过 *myfile.txt* 文件中的前两个标记，然后将第三个标记传递给 [**dds**](dds--dps--dqs--display-words-and-symbols-.md)。 每个令牌在传递后将跳过四个令牌。 结果就是将 **dds** 用于第三、第8、第13、18和23日标记等：

```dbgcmd
0:000> .foreach /pS 2 /ps 4 /f ( place "g:\myfile.txt") { dds place } 
```

有关使用 **foreach** 标记的更多示例，请参阅 [调试器命令程序示例](debugger-command-program-examples.md)。

 

 





