---
title: dv （显示本地变量）
description: Dv 命令显示当前作用域中的名称和值的所有本地变量。
ms.assetid: 1b5260f7-f47c-481a-b93f-015ab9fa4b58
keywords:
- dv （显示本地变量） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dv (Display Local Variables)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b4e17826565a066df5572d392a32008929e9169
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533761"
---
# <a name="dv-display-local-variables"></a>dv （显示本地变量）


**Dv**命令在当前范围内显示的名称和值的所有本地变量。

```dbgcmd
dv [Flags] [Pattern] 
```

## <a name="span-idddkcmddisplaylocalvariablesdbgspanspan-idddkcmddisplaylocalvariablesdbgspanparameters"></a><span id="ddk_cmd_display_local_variables_dbg"></span><span id="DDK_CMD_DISPLAY_LOCAL_VARIABLES_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
导致要显示的其他信息。 区分大小写以下任一*标志*可以包含：

<span id="_f__addr_"></span><span id="_F__ADDR_"></span>**/f** &lt;addr&gt;  
允许您指定的任意函数地址，以便您可以看到哪些参数和局部变量存在的任何位置的任何代码。 它将值显示关闭并意味着 **/V**。 **/F**标志必须为最后一个标志。 如果字符串括在引号，仍可以在其后指定参数筛选器模式。

<span id="_i"></span><span id="_I"></span>**/i**  
将导致显示可以指定变量的类型： 本地、 全局、 参数、 函数或未知。

<span id="_t"></span><span id="_T"></span>**/t**  
将导致显示以包括每个本地变量的数据类型。

<span id="_v"></span><span id="_V"></span>**/v**  
将导致显示要包含的虚拟内存地址或注册的每个本地变量的位置。

<span id="_V"></span><span id="_v"></span>**/V**  
与相同 **/v**，并且还包括相对于相关注册本地变量的地址。

<span id="_a"></span><span id="_A"></span>**/a**  
对输出进行排序的地址，按升序排序。

<span id="_A"></span><span id="_a"></span>**/A**  
对输出的地址，以降序进行排序。

<span id="_n"></span><span id="_N"></span>**/n**  
对输出进行排序的名称，按升序排序。

<span id="_N"></span><span id="_n"></span>**/N**  
对输出的名称，以降序进行排序。

<span id="_z"></span><span id="_Z"></span>**/z**  
对输出进行排序的大小，按升序排序。

<span id="_Z"></span><span id="_z"></span>**/Z**  
对输出的大小，以降序进行排序。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *Pattern*   
使命令仅显示具有指定的本地变量*模式*。 此模式可包含各种通配符和说明符;请参阅[字符串通配符语法](string-wildcard-syntax.md)有关详细信息。 如果*模式*包含空格，则必须用引号引起来。 如果*模式*是省略，就会显示所有本地变量。

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

显示和更改本地变量和其他与内存相关的命令的说明的详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

在详细模式下，还显示变量的地址。 (也可以使用实现这[ **（检查符号） x** ](x--examine-symbols-.md)命令。)

数据结构和不熟悉的数据类型不会显示在完整;而被显示其类型名称。 若要显示的整个结构或显示结构中的特定成员，请使用[ **dt （显示类型）** ](dt--display-type-.md)命令。

*本地上下文*确定将显示的一组的本地变量。 默认情况下，此上下文匹配程序计数器的当前位置。 有关如何更改此信息，请参阅[本地上下文](changing-contexts.md#local-context)。

 

 





