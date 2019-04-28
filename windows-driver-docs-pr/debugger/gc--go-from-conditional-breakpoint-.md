---
title: gc（从条件断点继续）
description: Gc 命令继续执行从条件断点命中断点 （单步执行、 跟踪、 或自由地执行） 所用的方式相同。
ms.assetid: 7850269a-3fc7-48b6-a369-bb020a5e11c3
keywords:
- gc （从条件性断点转） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gc (Go from Conditional Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 79095e76fcd3a683ed45e2ab7511c86d9a6e92f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347097"
---
# <a name="gc-go-from-conditional-breakpoint"></a>gc（从条件断点继续）


**Gc**命令继续执行从条件断点命中断点 （单步执行、 跟踪，或自由地执行） 所用的方式相同。

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

相关命令的概述，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

当[条件断点](setting-a-conditional-breakpoint.md)包括执行命令在结束时，这应该是**gc**命令。

例如，下面是正确的条件断点表述：

```dbgcmd
0:000> bp Address "j (Condition) 'OptionalCommands'; 'gc' " 
```

如果遇到此断点，表达式为 false，则将继续执行，使用以前使用过的同一个执行类型。 例如，如果您使用**g （转向）** 命令来达到此断点，执行将继续免费。 但如果单步执行或跟踪时达到此断点，执行将继续执行步骤或跟踪。

但是，下面是不正确的断点表述，因为即使你有已单步执行到达断点之前，始终将自由地继续执行：

```dbgcmd
0:000> bp Address "j (Condition) 'OptionalCommands'; 'g' " 
```

 

 





