---
title: ks.enumdrvobj
description: Ks.enumdrvobj 扩展显示与给定的 WDM 驱动程序对象关联的所有 KSDEVICE 结构，并列出的筛选器类型和当前实例化这些设备上的筛选器。
ms.assetid: 8fcb8c83-48b6-402a-8374-6b1f0314837e
keywords:
- ks.enumdrvobj Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.enumdrvobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cfd0360f4136e74d60ab14057f1ab0c725a7ba89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523376"
---
# <a name="ksenumdrvobj"></a>!ks.enumdrvobj


**！ Ks.enumdrvobj**扩展显示与给定的 WDM 驱动程序对象关联的所有 KSDEVICE 结构并列出了筛选器类型以及筛选器当前在这些设备上实例化。

```dbgcmd
!ks.enumdrvobj DriverObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DriverObject______"></span><span id="_______driverobject______"></span><span id="_______DRIVEROBJECT______"></span> *DriverObject*   
指定指向 WDM 驱动程序对象的指针。

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

由于 **！ ks.enumdrvobj**枚举链接关闭 WDM 驱动程序对象的所有设备它相当于调用[ **！ ks.enumdevobj** ](-ks-enumdevobj.md)链接关闭每个设备上给定驱动程序。

 

 





