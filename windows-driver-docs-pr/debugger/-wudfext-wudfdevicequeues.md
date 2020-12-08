---
title: wudfext.wudfdevicequeues
description: Wudfext. wudfdevicequeues 扩展显示有关设备的所有 i/o 队列的信息。
keywords:
- wudfext wudfdevicequeues Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdevicequeues
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce6dccd0664ae3bfe8ef5a82c5bf3d9da037b8d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794085"
---
# <a name="wudfextwudfdevicequeues"></a>!wudfext.wudfdevicequeues


**！ Wudfext wudfdevicequeues** 扩展显示有关设备的所有 i/o 队列的信息。

```dbgcmd
!wudfext.wudfdevicequeues pWDFDevice
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______pWDFDevice______"></span><span id="_______pwdfdevice______"></span><span id="_______PWDFDEVICE______"></span>*pWDFDevice*   
指定要显示其所有关联 i/o 队列相关信息的 **IWDFDevice** 接口的地址。 [**！ Wudfext wudfdriverinfo**](-wudfext-wudfdriverinfo.md) extension 命令确定 **IWDFDevice** 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面是 **！ wudfext** 显示的示例：

```dbgcmd
## kd> !wudfdevicequeues 0xf2f80 
--------------------------------------------------
Queue: 1 (!wudfqueue 0x000f3500)
    WdfIoQueueDispatchSequential, POWER MANAGED, WdfIoQueuePowerOn, CAN ACCEPT, CAN DISPATCH
    Number of driver owned requests: 1
      IWDFIoRequest 0x000fa7c0     CWdfIoRequest 0x000fa748
    Number of waiting requests: 199
      IWDFIoRequest 0x000fa908     CWdfIoRequest 0x000fa890
      IWDFIoRequest 0x000faa50     CWdfIoRequest 0x000fa9d8
...
      IWDFIoRequest 0x000fa678     CWdfIoRequest 0x000fa600
    Driver's callback interfaces.
      IQueueCallbackRead 0x000f343c
      IQueueCallbackDeviceIoControl 0x000f3438
      IQueueCallbackWrite 0x000f3440
```

 

 





