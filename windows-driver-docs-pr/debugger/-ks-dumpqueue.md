---
title: ks.dumpqueue
description: Ks.dumpqueue 扩展显示有关与给定 AVStream 对象关联的队列或与 port 类对象相关联的流的信息。
ms.assetid: d641b4e6-73d9-4c44-b2c6-0b6c688da368
keywords:
- ks.dumpqueue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumpqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed7a37d652f4b91abec804e45a75ee91a46dac7f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336302"
---
# <a name="ksdumpqueue"></a>!ks.dumpqueue


**！ Ks.dumpqueue**扩展显示有关与给定 AVStream 对象关联的队列或与 port 类对象相关联的流的信息。

```dbgcmd
!ks.dumpqueue Object [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
指定指向要为其显示队列对象的指针。 *对象*必须为类型 PKSPIN，PKSFILTER，CKsPin\*，CKsFilter\*，CKsQueue\*，CPortPin\*，或 CPortFilter\*。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *级别*   
可选。 指定要显示在 0 到 7 的详细信息级别越来越多的信息显示为较高的值的小数位数。 若要显示所有可用的详细信息，请提供值为 7。

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

*对象*必须是一个筛选器或 pin。 Pin，对于显示单个队列。 筛选器，显示了多个队列。

此命令可能需要一些时间执行。

下面是举例 **！ ks.dumpqueue**显示：

```dbgcmd
kd> !dumpqueue 829493c4
Filter 829493c4: Output Queue 82990e20:
 Queue 82990e20:
        Frames Received  : 1889
        Frames Waiting   : 3
        Frames Cancelled : 0
        And Gate 82949464 : count = 1, next = 00000000
    Frame Gate NULL
        Frame Header 82aaef78:
 NextFrameHeaderInIrp = 00000000
            OriginalIrp = 82169e48
            Mdl = 8292e358
            Irp = 82169e48
 StreamHeader = 8298dea0
            FrameBuffer = edba3000
            StreamHeaderSize = 00000000
            FrameBufferSize = 00025800
            Context = 00000000
            Refcount = 1
```

 

 





