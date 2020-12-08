---
title: ks. dumpcircuit
description: Dumpcircuit 扩展列出与给定对象关联的传输线路的详细信息。
keywords:
- dumpcircuit Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumpcircuit
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ddea681a9197e1932ac10b5f17f827d098f86d95
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787057"
---
# <a name="ksdumpcircuit"></a>!ks.dumpcircuit


**Dumpcircuit** 扩展列出与给定对象关联的传输线路的详细信息。

```dbgcmd
!ks.dumpcircuitextension Object [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span>*对象*   
指定一个指针，该指针指向要显示其传输线路的对象。 对于 AVStream， *对象* 必须是以下类型之一： CKsPin \* 、CKsQueue \* 、CKsRequestor \* 、CKsSplitter \* 、CKsSplitterBranch \* 。

对于 PortCls，对象必须是以下类型之一： CPortPin \* 、CKsShellRequestor \* 或 CIrpStream \* 。

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

请注意， **！ dumpcircuit** 开始遍历指定对象处的线路，这并不总是对应于数据源。

首先，可以将 [**！ ks**](-ks-graph.md) 与筛选器地址配合使用来列出 pin 地址，然后将这些地址用于 **！ dumpcircuit**。

下面是一个 **dumpcircuit** 显示示例：

```dbgcmd
kd> !dumpcircuit 8293f4f0
Pin8293f4f0 0 (snk, out)
Queue82990e20 r/w/c=2489/2/0
```

 

 





