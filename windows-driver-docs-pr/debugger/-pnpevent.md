---
title: pnpevent
description: Pnpevent 扩展显示插设备事件队列。
ms.assetid: 5f70fbf8-1313-4238-a917-c3fba8c80927
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
ms.openlocfilehash: 19c66eea6a61217ce7d7ca7c8fd498b28c7caeae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334356"
---
# <a name="pnpevent"></a>!pnpevent


**！ Pnpevent**扩展显示插设备事件队列。

```dbgcmd
!pnpevent [DeviceEvent]
```

## <a name="span-idddkpnpeventdbgspanspan-idddkpnpeventdbgspanparameters"></a><span id="ddk__pnpevent_dbg"></span><span id="DDK__PNPEVENT_DBG"></span>参数


<span id="_______DeviceEvent______"></span><span id="_______deviceevent______"></span><span id="_______DEVICEEVENT______"></span> *DeviceEvent*   
指定要显示的设备事件的地址。 如果这是零或省略，将显示在队列中的所有设备事件的树。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 有关插驱动程序的信息，请参阅 Windows Driver Kit (WDK) 文档。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[Plug and Play 和电源调试器命令](plug-and-play-and-power-debugger-commands.md)

 

 






