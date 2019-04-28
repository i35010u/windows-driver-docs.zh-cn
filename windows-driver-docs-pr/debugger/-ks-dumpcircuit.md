---
title: ks.dumpcircuit
description: Ks.dumpcircuit 扩展列出与给定对象关联的传输线路的详细信息。
ms.assetid: 34e6fa0f-7479-4616-ba7e-f2b12ccc836d
keywords:
- ks.dumpcircuit Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumpcircuit
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8167c78550aba9893f601632370aaa963faf98f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336301"
---
# <a name="ksdumpcircuit"></a>!ks.dumpcircuit


**！ Ks.dumpcircuit**扩展列出与给定对象关联的传输线路的详细信息。

```dbgcmd
!ks.dumpcircuitextension Object [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
指定指向要为其显示传输线路对象的指针。 有关 AVStream，*对象*必须是以下类型之一：CKsPin\*，CKsQueue\*，CKsRequestor\*，CKsSplitter\*，CKsSplitterBranch\*。

有关 PortCls，对象必须是以下类型之一：CPortPin\*，CKsShellRequestor\*，或 CIrpStream\*。

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

请注意， **！ ks.dumpcircuit**启动不始终对应于数据源的指定对象的每个步骤线路。

您可以首先使用[ **！ ks.graph** ](-ks-graph.md)列出 pin 地址，然后使用这些地址与筛选器地址 **！ ks.dumpcircuit**。

下面是举例 **！ ks.dumpcircuit**显示：

```dbgcmd
kd> !dumpcircuit 8293f4f0
Pin8293f4f0 0 (snk, out)
Queue82990e20 r/w/c=2489/2/0
```

 

 





