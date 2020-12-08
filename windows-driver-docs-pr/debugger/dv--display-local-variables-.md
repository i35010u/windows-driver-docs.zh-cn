---
title: dv（显示局部变量）
description: Dv 命令显示当前范围内的所有局部变量的名称和值。
keywords:
- dv (显示 Windows 调试) 本地变量
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dv (Display Local Variables)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 21848d9e8749a2d890bb15eb1938b19541b44471
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838658"
---
# <a name="dv-display-local-variables"></a>dv（显示局部变量）


**Dv** 命令显示当前范围内的所有局部变量的名称和值。

```dbgcmd
dv [Flags] [Pattern] 
```

## <a name="span-idddk_cmd_display_local_variables_dbgspanspan-idddk_cmd_display_local_variables_dbgspanparameters"></a><span id="ddk_cmd_display_local_variables_dbg"></span><span id="DDK_CMD_DISPLAY_LOCAL_VARIABLES_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
导致显示附加信息。 可以包括以下任何区分大小写的 *标志* ：

<span id="_f__addr_"></span><span id="_F__ADDR_"></span>**/f** &lt;addr&gt;  
允许您指定任意函数地址，以便您可以查看任何位置存在的任何代码的参数和局部变量。 它关闭值显示，并隐含 **/v**。 **/F** 标志必须是最后一个标志。 如果对字符串进行了引号，则仍可在参数筛选器模式后面指定该模式。

<span id="_i"></span><span id="_I"></span>**/i**  
使显示指定变量的类型： local、global、parameter、function 或 unknown。

<span id="_t"></span><span id="_T"></span>**/t**  
使显示包含每个局部变量的数据类型。

<span id="_v"></span><span id="_V"></span>**/v**  
使显示包括每个本地变量的虚拟内存地址或寄存器位置。

<span id="_V"></span><span id="_v"></span>**/V**  
与 **/v** 相同，还包括与相关寄存器相关的本地变量的地址。

<span id="_a"></span><span id="_A"></span>**/a**  
按地址升序排序输出。

<span id="_A"></span><span id="_a"></span>**/A**  
按地址按降序对输出进行排序。

<span id="_n"></span><span id="_N"></span>**/n**  
按名称按升序对输出进行排序。

<span id="_N"></span><span id="_n"></span>**/N**  
按名称以降序对输出进行排序。

<span id="_z"></span><span id="_Z"></span>**/z**  
按大小以升序对输出进行排序。

<span id="_Z"></span><span id="_z"></span>**/Z**  
按大小降序对输出进行排序。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*模式*   
使命令只显示与指定 *模式* 匹配的局部变量。 此模式可能包含各种通配符和说明符;有关详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md) 。 如果 *模式* 包含空格，则必须用引号将其引起来。 如果省略 *模式* ，则将显示所有局部变量。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关显示和更改本地变量的详细信息以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

在详细模式下，还会显示变量的地址。  (还可以通过 [**x (检查符号)**](x--examine-symbols-.md) 命令来完成此操作。 ) 

数据结构和不熟悉的数据类型不会全部显示;而是显示其类型名称。 若要显示整个结构，或显示结构的特定成员，请使用 [**dt (显示类型)**](dt--display-type-.md) 命令。

*本地上下文* 决定将显示哪一组局部变量。 默认情况下，此上下文与程序计数器的当前位置匹配。 有关如何更改此操作的信息，请参阅 [本地上下文](changing-contexts.md#local-context)。

 

 





