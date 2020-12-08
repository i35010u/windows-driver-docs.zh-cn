---
title: .asd
description: .Asd 扩展在从指定地址开始的数据缓存中显示指定数量的失败分析条目。
keywords:
- 从数据缓存显示的故障分析条目
- .asd Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- asd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 78c079e519734b01cf29f5dbcf394d91f9535b3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800021"
---
# <a name="asd"></a>!asd


**！ .Asd** 扩展在从指定地址开始的数据缓存中显示指定数量的失败分析条目。

```dbgcmd
    !asd Address DataUsed
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的第一个失败分析条目的地址。

<span id="_______DataUsed______"></span><span id="_______dataused______"></span><span id="_______DATAUSED______"></span>*DataUsed*   
确定要显示的令牌数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

您可以使用 [**！ dumpfa**](-dumpfa.md) 扩展名调试 [**！分析**](-analyze.md) 扩展。

<a name="remarks"></a>备注
-------

仅当调试 [**！分析**](-analyze.md)扩展时，才能用到 **！ .asd** 扩展。

 

 





