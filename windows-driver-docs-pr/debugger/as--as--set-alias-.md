---
title: as、aS（设置别名）
description: As 和 aS 命令定义一个新别名或重新定义一个别名。
keywords:
- 作为 (设置别名) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- as, aS (Set Alias)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 831ac07d459752e1271f75e8ad42a5123ba8dddd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819309"
---
# <a name="as-as-set-alias"></a>as、aS（设置别名）


**As** 和 **as** 命令定义一个新别名或重新定义一个别名。

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

## <a name="span-idddk_cmd_set_alias_dbgspanspan-idddk_cmd_set_alias_dbgspanparameters"></a><span id="ddk_cmd_set_alias_dbg"></span><span id="DDK_CMD_SET_ALIAS_DBG"></span>参数


<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span>*名称*   
指定别名。 此名称可以是不包含空格的任何文本字符串，也可以是 "al"、"as"、"aS" 或 "ad" 开头的任何文本字符串。 *名称* 区分大小写。

<span id="_______EquivalentLine______"></span><span id="_______equivalentline______"></span><span id="_______EQUIVALENTLINE______"></span>*EquivalentLine*   
指定等效的别名。 *EquivalentLine* 区分大小写。 至少必须在 *Name* 和 *EquivalentLine* 之间添加一个空格。 这两个参数之间的空格数并不重要。 等效的别名绝不会包含前导空格。 在这些空格之后， *EquivalentLine* 包括行的其余部分。 分号、引号和空格被视为文本字符，并包含尾随空格。

<span id="_______EquivalentPhrase______"></span><span id="_______equivalentphrase______"></span><span id="_______EQUIVALENTPHRASE______"></span>*EquivalentPhrase*   
指定等效的别名。 *EquivalentPhrase* 区分大小写。 至少必须在 *Name* 和 *EquivalentPhrase* 之间添加一个空格。 这两个参数之间的空格数并不重要。 等效的别名绝不会包含前导空格。

可以用引号将 *EquivalentPhrase* 括起来 ( ") 。 无论是否使用引号， *EquivalentPhrase* 都可以包含空格、逗号和单引号 ( ") 。 如果将 *EquivalentPhrase* 括在引号中，则它可以包含分号，但不能包含其他引号。 如果不将 *EquivalentPhrase* 括在引号中，则它可以在第一个字符之外的任何位置添加引号，但它不能包含分号。 不管是否使用引号，都包含尾随空格。

<span id="________e______"></span><span id="________E______"></span>**/e**   
将等效于 *value* 指定的环境变量的别名设置为。

<span id="_______EnvironmentVariable______"></span><span id="_______environmentvariable______"></span><span id="_______ENVIRONMENTVARIABLE______"></span>*Value*   
指定用于确定别名等效项的环境变量。 使用调试器的环境，而不是目标的。 如果在命令提示符窗口中启动了调试器，则使用该窗口中的环境变量。

<span id="________ma______"></span><span id="________MA______"></span>**/ma**   
将等效的别名设置为以 null 结尾的 ASCII 字符串（在 *Address* 开头）。

<span id="________mu______"></span><span id="________MU______"></span>**/mu**   
将等效的别名设置为以 null 结尾的 Unicode 字符串（从 *Address* 开始）。

<span id="________msa______"></span><span id="________MSA______"></span>**/msa**   
将等效于位于地址的 ANSI 字符串结构的别名设置为 \_ 。 *Address*

<span id="________msu______"></span><span id="________MSU______"></span>**/msu**   
将等效的别名设置为 \_ 位于 *地址* 的 UNICODE 字符串结构。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定用于确定别名等效项的虚拟内存位置。

<span id="________x______"></span><span id="________X______"></span>**/x**   
将等效的别名设置为等于64位值的 *Expression*。

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
指定要计算的表达式。 此值将成为等效的别名。 有关语法的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

<span id="________f______"></span><span id="________F______"></span>**/f**   
设置与 *文件* 文件内容等效的别名。 应始终将 **/f** 开关与 **as** 一起使用，而不是使用 **作为**。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span>*文件*   
指定其内容将变为别名等效项的文件。 *文件* 可以包含空格，但不应将 *文件* 括在引号中。 如果指定的文件无效，则会收到 "内存不足" 错误消息。

<span id="________c______"></span><span id="________C______"></span>**/c**   
将等效于 *command.commandstring* 指定的命令输出的别名设置为。 等效的别名包括回车符（如果它们存在于命令显示内）以及每个命令的显示末尾处的回车符（即使仅指定了一个命令) ） (。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span>*Command.commandstring*   
指定其输出将成为等效别名的命令。 此字符串可以包含任意数量的命令（用分号分隔）。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何使用别名的详细信息，请参阅 [使用别名](using-aliases.md)。

<a name="remarks"></a>备注
-------

如果不使用任何开关， **as** 命令将使用该行的其余部分作为等效的别名。

可以用分号结束 **aS** 命令。 当必须将所有命令放在一行上时，此方法在脚本中很有用。 请注意，如果分号后的行部分要求展开别名，则必须将该行的第二部分置于新块中。 下面的示例生成预期的输出0x6。

```dbgcmd
0:001> aS /x myAlias 5 + 1; .block{.echo myAlias}
0x6
```

如果省略新块，则不会获得预期的输出。 这是因为在输入新的代码块之前，不会出现新设置的别名。 在下面的示例中，省略了新块，输出为文本 "myAlias"，而不是预期的值0x6。

```dbgcmd
0:001> aS /x myAlias 5 + 1; .echo myAlias
myAlias
```

有关在脚本中使用别名的详细信息，请参阅 [使用别名](using-aliases.md)。

如果使用的是 **/e**、 **/ma**、 **/mu**、 **/msa**、 **/msu** 或 **/x** 开关，as 和 **as** 命令的工作 **方式** 相同，并且在遇到分号时命令结束。

如果 *name* 已是现有别名的名称，则重定义该别名。

可以使用 **as** 或 **as** 命令来创建或更改任何用户命名的别名。 但不能使用命令控制固定名称别名 ($u 0 $u 9) 。

可使用 **/ma**、 **/mu**、 **/msa**、 **/msu**、 **/f** 和 **/c** 开关创建包含回车符的别名。 但是，不能使用包含回车符的别名按顺序执行多个命令。 相反，必须使用分号。

 

 





