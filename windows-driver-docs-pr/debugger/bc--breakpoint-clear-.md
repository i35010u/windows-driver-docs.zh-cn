---
title: bc（断点清除）
description: Bc 命令从永久删除以前设置断点系统。
ms.assetid: 7bff5261-179f-4fd6-b427-de74e830a8c7
keywords:
- bc (断点清除) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bc (Breakpoint Clear)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5601e6bd150011861b40d7d80aab98650063f000
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357025"
---
# <a name="bc-breakpoint-clear"></a>bc（断点清除）


**Bc**命令永久删除以前从系统中设置断点。

```dbgcmd
bc Breakpoints 
```

## <a name="span-idddkcmdbreakpointcleardbgspanspan-idddkcmdbreakpointcleardbgspanparameters"></a><span id="ddk_cmd_breakpoint_clear_dbg"></span><span id="DDK_CMD_BREAKPOINT_CLEAR_DBG"></span>参数


<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span> *断点*   
指定要删除的断点的 ID 号。 可以指定任意数量的断点。 您必须将多个 Id 用空格或逗号。 可以使用连字符指定断点 Id 的范围 （-）。 可以使用星号 (\*) 以指示所有断点。 如果你想要使用[数值表达式](numerical-expression-syntax.md)id，请将其括在方括号中 (\[\])。 如果你想要使用[带有通配符字符的字符串](string-wildcard-syntax.md)以匹配断点的符号名称，请将其括在引号 ("")。

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
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何使用断点、 其他断点的命令和控制断点的方法以及如何从内核调试程序在用户空间中设置断点的详细信息，请参阅[使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

使用[ **bl （断点列表）** ](bl--breakpoint-list-.md)命令列出所有现有断点、 它们的 ID 号，以及它们的状态。

使用[ **.bpcmds （显示断点命令）** ](-bpcmds--display-breakpoint-commands-.md)命令列出所有现有断点、 它们的 ID 号，以及用于创建它们的命令。

 

 





