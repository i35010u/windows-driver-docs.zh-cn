---
title: ks. enumdevobj
description: Enumdevobj 扩展显示与给定 WDM 设备对象关联的 KSDEVICE，并列出当前在此设备上实例化的筛选器类型和筛选器。
keywords:
- enumdevobj Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.enumdevobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 38a6e15a78f53dcd5becdcf294e4128561e4bcb8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792433"
---
# <a name="ksenumdevobj"></a>!ks.enumdevobj


**Enumdevobj** 扩展显示与给定 WDM 设备对象关联的 KSDEVICE，并列出当前在此设备上实例化的筛选器类型和筛选器。

```dbgcmd
!ks.enumdevobj DeviceObject 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span>*DeviceObject*   
指定指向 WDM 设备对象的指针。

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

从 [**！ allstreams**](-ks-allstreams.md) 的输出可以用作 **！ enumdevobj** 的输入。

下面是一个 **enumdevobj** 显示示例：

```dbgcmd
kd> !enumdevobj 8241c020
WDM device object 8241c020:
    Corresponding KSDEVICE        823b8430
    Factory 829782dc [Descriptor f7a233c8] instances:
        829493c4 
```

 

 





