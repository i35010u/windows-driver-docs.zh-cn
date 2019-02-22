---
title: ks.dumpbag
description: Ks.dumpbag 扩展显示指定的对象的对象包的内容。
ms.assetid: a97b4794-b5dc-45a8-b1e9-5a626959020e
keywords:
- ks.dumpbag Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumpbag
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fcedf397edb4a3f1fbfc529f87a23987b921620b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547618"
---
# <a name="ksdumpbag"></a>!ks.dumpbag


**！ Ks.dumpbag**扩展将显示指定的对象的对象包的内容。

```dbgcmd
!ks.dumpbag Object [Level]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
指定为有效的客户端查看对象结构，或私有类对象的指针。

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

下面是举例 **！ ks.dumpbag**显示筛选器：

```dbgcmd
kd> !dumpbag 829493c4
Filter 829493c4 [CKsFilter = 82949350]:
    Object Bag 829493d0:
        Object Bag Item 829dce28:
            Reference Count        : 1
            Item Cleanup Handler   : f7a21730
```

 

 





