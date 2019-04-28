---
title: wudfext.wudfdevicequeues
description: Wudfext.wudfdevicequeues 扩展显示有关设备的所有 I/O 队列的信息。
ms.assetid: 985e6d93-018f-436a-a75c-088251398539
keywords:
- wudfext.wudfdevicequeues Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdevicequeues
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef0bce7454c02dd7e0fcc096a128aac9e9b173e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347933"
---
# <a name="wudfextwudfdevicequeues"></a>!wudfext.wudfdevicequeues


**！ Wudfext.wudfdevicequeues**扩展显示有关设备的所有 I/O 队列的信息。

```dbgcmd
!wudfext.wudfdevicequeues pWDFDevice
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______pWDFDevice______"></span><span id="_______pwdfdevice______"></span><span id="_______PWDFDEVICE______"></span> *pWDFDevice*   
指定的地址**IWDFDevice**要为其显示其相关联的 I/O 队列的所有信息的接口。 [ **！ Wudfext.wudfdriverinfo** ](-wudfext-wudfdriverinfo.md)扩展命令确定地址**IWDFDevice**。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

以下是一种 **！ wudfext.wudfdevicequeues**显示：

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

 

 





