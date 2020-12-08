---
title: bc（断点清除）
description: Bc 命令永久地从系统中删除以前设置的断点。
keywords:
- ) Windows 调试中的 bc (断点清除
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bc (Breakpoint Clear)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: db67eb1823ccdd86d8d0eb398e0ad1617262967f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838375"
---
# <a name="bc-breakpoint-clear"></a>bc（断点清除）


**Bc** 命令永久地从系统中删除以前设置的断点。

```dbgcmd
bc Breakpoints 
```

## <a name="span-idddk_cmd_breakpoint_clear_dbgspanspan-idddk_cmd_breakpoint_clear_dbgspanparameters"></a><span id="ddk_cmd_breakpoint_clear_dbg"></span><span id="DDK_CMD_BREAKPOINT_CLEAR_DBG"></span>参数


<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span>*断点*   
指定要删除的断点的 ID 号。 可以指定任意数量的断点。 必须用空格或逗号分隔多个 Id。 可以通过使用连字符 ( ) 来指定断点 Id 的范围。 可以使用星号 (\*) 来指示所有断点。 如果要对 ID 使用[数值表达式](numerical-expression-syntax.md)，请将其括在括号中， (\[ \]) 。 如果要使用 [带有通配符的字符串](string-wildcard-syntax.md) 来匹配断点的符号名称，请将其括在引号中 ( "" ) 。

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
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要详细了解如何使用断点、其他断点命令和控制断点的方法，以及如何在用户空间中从内核调试器设置断点，请参阅 [使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

使用 [**bl (断点列表)**](bl--breakpoint-list-.md) 命令可列出所有现有断点、其 ID 号及其状态。

使用 [**bpcmds (显示断点命令)**](-bpcmds--display-breakpoint-commands-.md) 命令可列出所有现有断点、其 ID 号以及用于创建它们的命令。

 

 





