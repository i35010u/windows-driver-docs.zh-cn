---
title: be（断点启用）
description: 将命令还原之前处于禁用状态的一个或多个断点。
ms.assetid: 110fe8b0-0bc7-49ce-9c66-326d5897c0ca
keywords:
- 是 （启用断点） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- be (Breakpoint Enable)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17f0ab8fcf782655dfee280abbe77a688f00026b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569117"
---
# <a name="be-breakpoint-enable"></a>be（断点启用）


**是**命令将还原之前处于禁用状态的一个或多个断点。

```dbgcmd
be Breakpoints 
```

## <a name="span-idddkcmdbreakpointenabledbgspanspan-idddkcmdbreakpointenabledbgspanparameters"></a><span id="ddk_cmd_breakpoint_enable_dbg"></span><span id="DDK_CMD_BREAKPOINT_ENABLE_DBG"></span>参数


<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span> *断点*   
指定要启用的断点的 ID 号。 可以指定任意数量的断点。 您必须将多个 Id 用空格或逗号。 可以使用连字符指定断点 Id 的范围 （-）。 可以使用星号 (**\\* * *) 以指示所有断点。如果你想要使用[数值表达式](numerical-expression-syntax.md)id，请将其括在方括号中 (*<em>\[\]</em><em>)。如果你想要使用[带有通配符字符的字符串](string-wildcard-syntax.md)若要匹配断点的符号名称，请将其括在引号 (**""</em>*  )。

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

有关详细信息和如何使用断点、 其他断点的命令和控制断点的方法以及如何从内核调试程序在用户空间中设置断点的示例，请参阅[使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

使用[ **bl （断点列表）** ](bl--breakpoint-list-.md)命令列出所有现有断点、 它们的 ID 号，以及它们的状态。

使用[ **.bpcmds （显示断点命令）** ](-bpcmds--display-breakpoint-commands-.md)命令列出所有现有断点、 它们的 ID 号，以及用于创建它们的命令。

 

 





