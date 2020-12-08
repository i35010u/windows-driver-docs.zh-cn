---
title: ks. devhdr
description: Devhdr 扩展显示与给定 WDM 对象关联的内核流式处理设备标头。
keywords:
- devhdr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.devhdr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 99c6372638604a3f7610d2ab0674c02b146f7b74
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792035"
---
# <a name="ksdevhdr"></a>!ks.devhdr


**Devhdr** 扩展显示与给定 WDM 对象关联的内核流式处理设备标头。

```dbgcmd
!ks.devhdr DeviceObject 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span>*DeviceObject*   
此参数指定指向 WDM 设备对象的指针。 如果 *DeviceObject* 无效，则该命令将返回一个错误。

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

从 [**！ allstreams**](-ks-allstreams.md) 的输出可以用作 **！ devhdr** 的输入。

下面是一个 **devhdr** 显示示例：

```dbgcmd
kd> !devhdr 827aedf0 7
Device Header 824ca1e0
    Child Create Handler List:
        Create Item eb3a7284
            CreateFunction = sysaudio!CFilterInstance::FilterDispatchCreate+0x00 
            ObjectClass = NULL
            Flags = 0
```

 

 





