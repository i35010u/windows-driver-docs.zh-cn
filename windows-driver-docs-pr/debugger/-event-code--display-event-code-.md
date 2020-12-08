---
title: .event_code（显示事件代码）
description: .Event_code 命令显示当前的事件说明。
keywords:
- .event_code (在 Windows 调试) 显示事件代码
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .event_code (Display Event Code)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 829d97c2855a2539470c777a12a04cb265664a9c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819435"
---
# <a name="event_code-display-event-code"></a>。事件 \_ 代码 (显示事件代码) 


**事件 \_ 代码** 命令显示当前的事件说明。

```dbgcmd
.event_code 
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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**事件 \_ 代码** 命令在当前事件的指令指针处显示十六进制指令。 如果可用，则显示的指令最多可包含64个字节。

 

 





