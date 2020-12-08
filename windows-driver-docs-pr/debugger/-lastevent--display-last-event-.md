---
title: .lastevent（显示最后一个事件）
description: Lastevent 命令显示最近发生的异常或事件。
keywords:
- lastevent (显示上一事件) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .lastevent (Display Last Event)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0bb68ef1526b4fdb5b048149afcea671ce40d85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818715"
---
# <a name="lastevent-display-last-event"></a>.lastevent（显示最后一个事件）


**Lastevent** 命令显示最近发生的异常或事件。

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
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关异常和事件的详细信息，请参阅 [控制异常和事件](controlling-exceptions-and-events.md)。

<a name="remarks"></a>备注
-------

中断到调试器始终会创建异常。 调试器接受命令输入时始终存在 *最后一个事件* 。 如果使用 [**ctrl + C**](ctrl-c--break-.md)、 [ctrl + break](debug---break.md)或 Debug 中断到调试器 |中断，将创建0x80000003 的异常代码。

 

 





