---
title: as、aS（设置别名）
description: As 和命令定义新的别名或重新定义现有。
ms.assetid: 6e42122b-5a18-403b-a19a-1346bea8da12
keywords:
- 如，作为 （集别名） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- as, aS (Set Alias)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc6fe184b81ddf621165be258a5c529c13bd40fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354695"
---
# <a name="as-as-set-alias"></a>as、aS（设置别名）


**作为**并**作为**命令定义新的别名或重新定义现有。

```dbgcmd
as Name EquivalentLine 
aS Name EquivalentPhrase 
aS Name "EquivalentPhrase" 
as /e Name EnvironmentVariable 
as /ma Name Address 
as /mu Name Address 
as /msa Name Address 
as /msu Name Address 
as /x Name Expression 
aS /f Name File 
as /c Name CommandString 
```

## <a name="span-idddkcmdsetaliasdbgspanspan-idddkcmdsetaliasdbgspanparameters"></a><span id="ddk_cmd_set_alias_dbg"></span><span id="DDK_CMD_SET_ALIAS_DBG"></span>参数


<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名称*   
指定的别名名称。 此名称可以是任何文本字符串不包含空格或 ENTER 键击和开头不为"al"，"为"，"为"或"ad"。 *名称*区分大小写。

<span id="_______EquivalentLine______"></span><span id="_______equivalentline______"></span><span id="_______EQUIVALENTLINE______"></span> *EquivalentLine*   
指定的别名等效项。 *EquivalentLine*区分大小写。 您必须至少一个之间添加空格*名称*并*EquivalentLine*。 这两个参数之间的空格数并不重要。 别名等效永远不会包含前导空格。 之后这些空格*EquivalentLine*包括行的其余内容。 包含分号、 引号和空格被视为原义字符和尾随空格。

<span id="_______EquivalentPhrase______"></span><span id="_______equivalentphrase______"></span><span id="_______EQUIVALENTPHRASE______"></span> *EquivalentPhrase*   
指定的别名等效项。 *EquivalentPhrase*区分大小写。 您必须至少一个之间添加空格*名称*并*EquivalentPhrase*。 这两个参数之间的空格数并不重要。 别名等效永远不会包含前导空格。

您可以将*EquivalentPhrase*用引号 （"）。 无论使用引号中， *EquivalentPhrase*可以包含空格、 逗号和单引号 （'） 引起来。 如果将括*EquivalentPhrase*在引号中，它可以包含分号，但不是额外的引号。 如果您不能将放*EquivalentPhrase*在引号中，它可以包含的第一个字符之外的任何位置中的引号，但它不能包含分号。 无论使用引号将包含尾随空格。

<span id="________e______"></span><span id="________E______"></span> **/e**   
环境变量设置别名等效相等*环境变量*指定。

<span id="_______EnvironmentVariable______"></span><span id="_______environmentvariable______"></span><span id="_______ENVIRONMENTVARIABLE______"></span> *EnvironmentVariable*   
指定用于确定等效的别名的环境变量。 使用调试器的环境，而不是目标的。 如果在命令提示符窗口在调试器中启动，则使用该窗口中的环境变量。

<span id="________ma______"></span><span id="________MA______"></span> **/ma**   
设置为以 null 结尾的 ASCII 字符串处开头的别名等效等*地址*。

<span id="________mu______"></span><span id="________MU______"></span> **/mu**   
将别名等效等号设置为以 null 结尾的 Unicode 字符串的开始处*地址*。

<span id="________msa______"></span><span id="________MSA______"></span> **/msa**   
将别名等效等号设置为 ANSI\_字符串结构，它是位于*地址*。

<span id="________msu______"></span><span id="________MSU______"></span> **/msu**   
将别名等效等号设置为 UNICODE\_字符串结构，它是位于*地址*。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定用于确定别名等效的虚拟内存位置。

<span id="________x______"></span><span id="________X______"></span> **/x**   
设置 64 位值的别名等效相等*表达式*。

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
指定要计算的表达式。 此值将成为该别名等效。 有关语法的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

<span id="________f______"></span><span id="________F______"></span> **/f**   
对内容的设置别名等效等*文件*文件。 应始终使用 **/f**一起使用切换**作为**，不能与**作为**。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span> *文件*   
指定其内容成为该别名文件等效。 *文件*可以包含空格，但应永远不会将括*文件*引号引起来。 如果指定了无效的文件，你会收到"内存不足"错误消息。

<span id="________c______"></span><span id="________C______"></span> **/c**   
命令的输出设置别名等效相等*CommandString*指定。 如果它们位于中的命令显示一个回车符 （即使您指定只有一个命令） 的每个命令显示的末尾返回，别名等效项包括回车。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定其输出成为别名命令等效。 此字符串可以包含任意数量的以分号分隔的命令。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何使用别名的详细信息，请参阅[Using 别名](using-aliases.md)。

<a name="remarks"></a>备注
-------

如果不使用任何开关**作为**命令行的其余内容使用为别名等效。

您可以结束**作为**命令由分号。 此方法时，在脚本中您必须将所有命令都放在单独的行。 请注意，是否分号后面的行的部分需要别名的扩展，必须在新的块中将行的第二个部分。 下面的示例生成预期的输出，0x6。

```dbgcmd
0:001> aS /x myAlias 5 + 1; .block{.echo myAlias}
0x6
```

如果省略新的块，则不会收到预期的输出。 这是因为扩展的新设置别名不会发生在输入新的代码块之前。 在以下示例中，省略新的块，而输出是文本而不是预期值 0x6"myAlias"。

```dbgcmd
0:001> aS /x myAlias 5 + 1; .echo myAlias
myAlias
```

有关在脚本中使用别名的详细信息，请参阅[Using 别名](using-aliases.md)。

如果您使用 **/e**， **/ma**， **/mu**， **/msa**， **/msu**，或 **/x**切换，请**作为**并**作为**命令的工作方式相同，如果遇到分号，则该命令将结束。

如果*名称*已经是一个现有的别名，别名被重新定义的名称。

可以使用**作为**或**作为**命令以创建或更改任何用户命名的别名。 但不能使用该命令来控制的固定名称别名 ($u0 到 $u9)。

可以使用 **/ma**， **/mu**， **/msa**， **/msu**， **/f**，和 **/c**交换机，以创建一个别名来包含回车符和返回。 但是，不能使用包含回车要按顺序执行多个命令的别名。 相反，您必须使用分号。

 

 





