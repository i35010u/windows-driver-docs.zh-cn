---
title: ks. forcedump
description: Forcedump 命令在调用方提供的地址上显示有关内存内容的信息。
keywords:
- forcedump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.forcedump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0c3abeaffb08ff8e152280ea84a6b4e4e74f1554
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828277"
---
# <a name="ksforcedump"></a>!ks.forcedump


**Forcedump** 命令在调用方提供的地址上显示有关内存内容的信息。

```dbgcmd
!ks.forcedump Object Type [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span>*对象*   
指定指向要显示其信息的对象的指针。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span>*类型*   
指定对象的类型。

对于 AVStream/KS 对象， *Type* 必须是以下值之一： CKsQueue、CKsDevice、CKsFilterFactory、CKsFilter、CKsPin、CKsRequestor、CKsSplitter、CKsSplitterBranch、CKsPipeSection、KSPIN、KSFILTER、KSFILTERFACTORY、KSDEVICE、KSSTREAM 指针、KSPFRAME 标头、KSIOBJECT 标头、KSPDO \_ \_ \_ EXTENSION、KSIDEVICE 标头、KSSTREAM 标头、KSPIN 描述符（CKsProxy \_ \_ 、CKsInputPin \_ \_ \_ 、CKsOutputPin、CasyncItemHandler）。

对于端口类对象， *Type* 必须是下列值之一： DEVICE \_ CONTEXT、CPortWaveCyclic、CPortPinWaveCyclic、CPortTopology、CPortDMus、CIrpStream、CKsShellRequestor、CPortFilterWaveCyclic、CDmaChannel、CPortWavePci、CportPinWavePci。

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

通常，可以使用 [**！ ks**](-ks-dump.md) 显示数据结构。

但是，如果未正确加载符号或分页出了太多的信息，则 [**！ ks. dump**](-ks-dump.md) 命令中的类型标识逻辑可能无法识别给定地址处的结构类型。

如果发生这种情况，请尝试使用 **forcedump** 命令。 此命令的工作方式与 [**！ ks**](-ks-dump.md) 相同，不同之处在于用户指定对象的类型。

**注意**  **Forcedump** 命令不会验证 *类型* 是否是在 *对象* 中提供的地址处找到的结构的正确类型。 命令假定这是在 *对象* 中找到的结构类型，并相应地显示数据。

 

可以通过发出不带参数的 **！ forcedump** 命令来检索所有支持的对象的列表。

下面是使用 *对象* 参数的筛选器地址的两个 **forcedump** 输出的示例，但详细级别不同：

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

 

 





