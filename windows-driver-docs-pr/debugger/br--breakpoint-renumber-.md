---
title: br（断点重新编号）
description: B 命令对一个或多个断点进行重新编号。
ms.assetid: 1b41eb37-3375-4203-bbf5-f55869383db8
keywords:
- br （断点重新编号） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- br (Breakpoint Renumber)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c53c99d28d259391fd85b44b745f3b069673a013
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347869"
---
# <a name="br-breakpoint-renumber"></a>br（断点重新编号）


**Br**命令对一个或多个断点进行重新编号。

```dbgcmd
br OldID NewID [OldID2 NewID2 ...] 
```

## <a name="span-idddkcmdbreakpointrenumberdbgspanspan-idddkcmdbreakpointrenumberdbgspanparameters"></a><span id="ddk_cmd_breakpoint_renumber_dbg"></span><span id="DDK_CMD_BREAKPOINT_RENUMBER_DBG"></span>参数


<span id="_______OldID______"></span><span id="_______oldid______"></span><span id="_______OLDID______"></span> *OldID*   
指定断点的当前 ID 号。

<span id="_______NewID______"></span><span id="_______newid______"></span><span id="_______NEWID______"></span> *NewID*   
指定的断点的 ID 将成为一个新数字。

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

可以使用**br**命令在同一时间重新编号任意数量的断点。 对于每个断点，请列出旧的 ID 和该顺序中的新 ID 作为参数**br**。

如果已存在具有 ID 等于的断点*NewID*，该命令将失败并显示一条错误消息。

 

 





