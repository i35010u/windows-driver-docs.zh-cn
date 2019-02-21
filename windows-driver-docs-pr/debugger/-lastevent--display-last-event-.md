---
title: .lastevent （显示最后一个事件）
description: .Lastevent 命令显示的最新的异常或发生的事件。
ms.assetid: 6f722c22-cb0f-4a10-b719-a168f7ba0943
keywords:
- .lastevent （显示最后一个事件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .lastevent (Display Last Event)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc4137f1aa7b2ed47a26aedaabd990995d15a0eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519807"
---
# <a name="lastevent-display-last-event"></a>.lastevent （显示最后一个事件）


**.Lastevent**命令显示的最新的异常或发生的事件。

```dbgcmd
.lastevent 
```

## <span id="ddk_meta_display_last_event_dbg"></span><span id="DDK_META_DISPLAY_LAST_EVENT_DBG"></span>


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

有关异常和事件的详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

<a name="remarks"></a>备注
-------

始终中断到调试器创建一个例外情况。 始终*最后一个事件*调试器接受命令输入的时间。 如果使用进入调试器[ **CTRL + C**](ctrl-c--break-.md)， [CTRL + BREAK](debug---break.md)，或调试 |创建 break，0x80000003 异常代码。

 

 





