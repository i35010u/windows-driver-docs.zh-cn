---
title: ks.forcedump
description: Ks.forcedump 命令显示有关内存内容的信息，在调用方提供的地址。
ms.assetid: 2829d324-a346-47af-a5f8-1808f329cadf
keywords:
- ks.forcedump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.forcedump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b423c675d4e5b9d5e50307eec9c0cafc5bc24c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336315"
---
# <a name="ksforcedump"></a>!ks.forcedump


**！ Ks.forcedump**命令显示有关内存内容的信息在调用方提供的地址。

```dbgcmd
!ks.forcedump Object Type [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
指定要显示其信息的对象的指针。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *Type*   
指定的对象的类型。

有关 AVStream/KS 对象*类型*必须是以下值之一：CKsQueue、 CKsDevice、 CKsFilterFactory、 CKsFilter、 CKsPin、 CKsRequestor、 CKsSplitter、 CKsSplitterBranch、 CKsPipeSection、 KSPIN、 KSFILTER、 KSFILTERFACTORY、 KSDEVICE、 KSSTREAM\_指针，KSPFRAME\_标头，KSIOBJECT\_标头、 KSPDO\_扩展，KSIDEVICE\_标头、 KSSTREAM\_标头、 KSPIN\_描述符\_EX、 CKsProxy、 CKsInputPin、 CKsOutputPin、 CasyncItemHandler。

端口类对象*类型*必须是以下值之一：设备\_上下文、 CPortWaveCyclic、 CPortPinWaveCyclic、 CPortTopology、 CPortDMus、 CIrpStream、 CKsShellRequestor、 CPortFilterWaveCyclic、 CDmaChannel、 CPortWavePci、 CportPinWavePci。

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

通常情况下，可以使用[ **！ ks.dump** ](-ks-dump.md)要显示的数据结构。

但是，如果未正确加载符号或过多信息调出中的类型标识逻辑[ **！ ks.dump** ](-ks-dump.md)命令可能会失败来标识在给定的地址结构的类型。

如果发生这种情况，请尝试使用 **！ ks.forcedump**命令。 此命令的工作方式类似[ **！ ks.dump** ](-ks-dump.md)只不过用户指定的对象类型。

**请注意**   **！ ks.forcedump**命令不会验证*类型*是正确类型的结构中提供的地址处找到*对象*. 该命令假定这是一种结构，请参阅*对象*并相应地显示数据。

 

可以通过发出检索所有支持的对象的列表 **！ ks.forcedump**命令不带任何参数。

以下是两个示例的输出 **！ ks.forcedump**，使用的筛选器的地址*对象*参数但具有不同级别的详细信息：

```dbgcmd
kd> !forcedump 829493c4 KSFILTER
WARNING: I am dumping 829493c4 as a KSFILTER.
         No checking has been performed to ensure that it is this type!!!

Filter object 829493c4 [CKsFilter = 82949350]
    Descriptor     f7a233c8:
    Context        829dce28

kd> !forcedump 829493c4 KSFILTER 7
WARNING: I am dumping 829493c4 as a KSFILTER.
         No checking has been performed to ensure that it is this type!!!

Filter object 829493c4 [CKsFilter = 82949350]
    Descriptor     f7a233c8:
    Filter Category GUIDs:
        Video
        Capture
    Context        829dce28
    INTERNAL INFORMATION:
        Public Parent Factory   829782dc
        Aggregated Unknown      00000000
        Device Interface        823b83c8
        Control Mutex           829493f8 is not held
    Object Event List:
        None
    CKsFilter object 82949350 [KSFILTER = 829493c4]
        Processing Mutex         82949484 is not held
        Gate &                   82949464
        Gate.Count               1
        Pin Factories:
            Pin ID 0 [Video/General Capture Out]:
                Child Count        1
                Bound Child Count  1
                Necessary Count    0
                Specific Instances:
                    8293f580 
```

 

 





