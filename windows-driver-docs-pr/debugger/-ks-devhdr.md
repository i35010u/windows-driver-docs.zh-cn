---
title: ks.devhdr
description: Ks.devhdr 扩展显示流式处理与给定的 WDM 对象关联的设备标头的内核。
ms.assetid: 1418ccfe-3842-422c-b2ce-124d0019d7b8
keywords:
- ks.devhdr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.devhdr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b2df61a97cf1b12eff226e84377116a7f514ad2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526662"
---
# <a name="ksdevhdr"></a>!ks.devhdr


**！ Ks.devhdr**扩展显示流式处理与给定的 WDM 对象关联的设备标头的内核。

```dbgcmd
!ks.devhdr DeviceObject 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
此参数指定指向 WDM 设备对象的指针。 如果*DeviceObject*不是有效的该命令将返回错误。

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

从输出[ **！ ks.allstreams** ](-ks-allstreams.md)可用作输入 **！ ks.devhdr**。

下面是举例 **！ ks.devhdr**显示：

```dbgcmd
kd> !devhdr 827aedf0 7
Device Header 824ca1e0
    Child Create Handler List:
        Create Item eb3a7284
            CreateFunction = sysaudio!CFilterInstance::FilterDispatchCreate+0x00 
            ObjectClass = NULL
            Flags = 0
```

 

 





