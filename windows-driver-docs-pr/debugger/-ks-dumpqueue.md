---
title: ks. dumpqueue
description: Dumpqueue 扩展显示与给定 AVStream 对象关联的队列或与端口类对象关联的流的相关信息。
keywords:
- dumpqueue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumpqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2709c9fbf933aee0020b0ec672077c40a9512bec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821045"
---
# <a name="ksdumpqueue"></a>!ks.dumpqueue


**Dumpqueue** 扩展显示与给定 AVStream 对象关联的队列或与端口类对象相关联的流的相关信息。

```dbgcmd
!ks.dumpqueue Object [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span>*对象*   
指定一个指针，该指针指向要显示其队列的对象。 *对象* 的类型必须是 PKSPIN、PKSFILTER、CKsPin \* 、CKsFilter \* 、CKsQueue \* 、CPortPin \* 或 CPortFilter \* 。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
可选。 指定要在0-7 刻度上显示的详细信息的级别，并为较高的值显示更多的信息。 若要显示所有可用的详细信息，请提供值7。

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

*对象* 必须是筛选器或 pin。 对于 pin，将显示单个队列。 对于筛选器，会显示多个队列。

执行此命令可能需要一段时间。

下面是一个 **dumpqueue** 显示示例：

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

 

 





