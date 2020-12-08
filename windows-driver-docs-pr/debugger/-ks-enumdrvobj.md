---
title: ks. enumdrvobj
description: Enumdrvobj 扩展显示与给定 WDM 驱动程序对象关联的所有 KSDEVICE 结构，并列出这些设备上当前实例化的筛选器类型和筛选器。
keywords:
- enumdrvobj Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.enumdrvobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 45812356b52cc1571d63ef7bd8ce6d9df9c3f6e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828301"
---
# <a name="ksenumdrvobj"></a>!ks.enumdrvobj


**Enumdrvobj** 扩展显示与给定 WDM 驱动程序对象关联的所有 KSDEVICE 结构，并列出这些设备上当前实例化的筛选器类型和筛选器。

```dbgcmd
!ks.enumdrvobj DriverObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DriverObject______"></span><span id="_______driverobject______"></span><span id="_______DRIVEROBJECT______"></span>*DriverObject*   
指定指向 WDM 驱动程序对象的指针。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核流调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

由于 **enumdrvobj** 枚举了链接到 WDM 驱动程序对象的每个设备，因此它等效于在与给定驱动程序链接的每个设备上调用 [**enumdevobj。**](-ks-enumdevobj.md)

 

 





