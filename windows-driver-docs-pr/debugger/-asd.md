---
title: asd
description: Asd 扩展显示指定的数目的失败分析从数据缓存，在指定地址开始的条目。
ms.assetid: fb0eeedd-d50b-4385-b35f-4ac46fb97ce0
keywords:
- 失败分析条目，显示从数据缓存
- asd Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- asd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 672a6cb35443fff4c4ec0c201bb38b0e1ae19313
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334748"
---
# <a name="asd"></a>!asd


**！ Asd**扩展显示指定的数目的失败分析从数据缓存，在指定地址开始的条目。

```dbgcmd
    !asd Address DataUsed
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的第一个故障分析条目的地址。

<span id="_______DataUsed______"></span><span id="_______dataused______"></span><span id="_______DATAUSED______"></span> *DataUsed*   
确定要显示的标记数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

可以使用[ **！ dumpfa** ](-dumpfa.md)扩展来调试[ **！ 分析**](-analyze.md)扩展。

<a name="remarks"></a>备注
-------

**！ Asd**扩展仅在调试非常有用[ **！ 分析**](-analyze.md)扩展。

 

 





