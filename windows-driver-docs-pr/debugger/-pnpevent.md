---
title: pnpevent
description: Pnpevent 扩展显示即插即用设备事件队列。
keywords:
- pnpevent Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pnpevent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25d4b3807c0feff4fa06ba6a4b1f0b08ff6a0ccb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822637"
---
# <a name="pnpevent"></a>!pnpevent


**！ Pnpevent** 扩展显示即插即用设备事件队列。

```dbgcmd
!pnpevent [DeviceEvent]
```

## <a name="span-idddk__pnpevent_dbgspanspan-idddk__pnpevent_dbgspanparameters"></a><span id="ddk__pnpevent_dbg"></span><span id="DDK__PNPEVENT_DBG"></span>参数


<span id="_______DeviceEvent______"></span><span id="_______deviceevent______"></span><span id="_______DEVICEEVENT______"></span>*DeviceEvent*   
指定要显示的设备事件的地址。 如果此值为零或省略，则显示队列中所有设备事件的树。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序。 有关即插即用驱动程序的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[即插即用和 Power 调试器命令](plug-and-play-and-power-debugger-commands.md)

 

 






