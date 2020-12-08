---
title: br（断点重新编号）
description: Br 命令对一个或多个断点进行编号。
keywords:
- ) Windows 调试时，br (断点重新编号
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- br (Breakpoint Renumber)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7376e3dad8db96e3333adec884e99e5975707bee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788899"
---
# <a name="br-breakpoint-renumber"></a>br（断点重新编号）


**Br** 命令对一个或多个断点进行编号。

```dbgcmd
br OldID NewID [OldID2 NewID2 ...] 
```

## <a name="span-idddk_cmd_breakpoint_renumber_dbgspanspan-idddk_cmd_breakpoint_renumber_dbgspanparameters"></a><span id="ddk_cmd_breakpoint_renumber_dbg"></span><span id="DDK_CMD_BREAKPOINT_RENUMBER_DBG"></span>参数


<span id="_______OldID______"></span><span id="_______oldid______"></span><span id="_______OLDID______"></span>*OldID*   
指定断点的当前 ID 号。

<span id="_______NewID______"></span><span id="_______newid______"></span><span id="_______NEWID______"></span>*NewID*   
指定成为断点 ID 的新编号。

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

有关如何使用断点、其他断点命令和控制断点的方法以及如何在用户空间中从内核调试器设置断点的详细信息，请参阅 [使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

您可以使用 **br** 命令同时对任意数量的断点重新进行编号。 对于每个断点，以该顺序列出旧 ID 和新 ID 作为 **br** 的参数。

如果已存在 ID 等于 *NewID* 的断点，则该命令将失败，并显示一条错误消息。

 

 





