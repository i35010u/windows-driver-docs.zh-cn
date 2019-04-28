---
title: ks.enumdevobj
description: Ks.enumdevobj 扩展显示与给定的 WDM 设备对象相关联 KSDEVICE 并列出的筛选器类型和当前实例化此设备上的筛选器。
ms.assetid: 3730fe3e-df7a-47fd-825b-ef31be6f7620
keywords:
- ks.enumdevobj Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.enumdevobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ca40efafbe61729d7adb6ec86f0f3d4f253d7b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336292"
---
# <a name="ksenumdevobj"></a>!ks.enumdevobj


**！ Ks.enumdevobj**扩展显示与给定的 WDM 设备对象相关联 KSDEVICE 并列出了筛选器类型以及筛选器当前在此设备上实例化。

```dbgcmd
!ks.enumdevobj DeviceObject 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
指定指向 WDM 设备对象的指针。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[流式处理的内核调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

从输出[ **！ ks.allstreams** ](-ks-allstreams.md)可用作输入 **！ ks.enumdevobj**。

下面是举例 **！ ks.enumdevobj**显示：

```dbgcmd
kd> !enumdevobj 8241c020
WDM device object 8241c020:
    Corresponding KSDEVICE        823b8430
    Factory 829782dc [Descriptor f7a233c8] instances:
        829493c4 
```

 

 





