---
title: gc（从条件断点继续）
description: Gc 命令从条件断点恢复执行，其方式与用于命中断点 (单步执行、跟踪或自由执行) 相同。
keywords:
- gc (从条件断点) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gc (Go from Conditional Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e124f5bf55e913b0d225cb4ceddc1763dd92d5cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837349"
---
# <a name="gc-go-from-conditional-breakpoint"></a>gc（从条件断点继续）


**Gc** 命令从条件断点恢复执行，其方式与用于命中断点 (单步执行、跟踪或自由执行) 相同。

```dbgcmd
gc
```

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令的概述，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

当 [条件断点](setting-a-conditional-breakpoint.md) 在末尾包含执行命令时，该命令应为 **gc** 命令。

例如，下面是适当的条件断点表述：

```dbgcmd
0:000> bp Address "j (Condition) 'OptionalCommands'; 'gc' " 
```

如果遇到此断点并且表达式为 false，则将使用以前使用的相同执行类型继续执行。 例如，如果使用了 **g (转)** 命令来到达此断点，则执行将可以自由地恢复。 但如果在单步执行或跟踪时到达此断点，则执行将继续执行步骤或跟踪。

另一方面，以下是不正确的断点表述，因为即使在到达断点之前已经单步执行，执行也将始终免费恢复：

```dbgcmd
0:000> bp Address "j (Condition) 'OptionalCommands'; 'g' " 
```

 

 





