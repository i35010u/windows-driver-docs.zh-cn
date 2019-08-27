---
title: tz
description: Tz 扩展显示指定的电源热量区域结构。
ms.assetid: f3cc9e54-a0db-4095-b707-380ec1dacf59
keywords:
- 热区
- tz Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tz
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f413108c5e30712958efd5cbabe9e46842c33b0
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025162"
---
# <a name="tz"></a>!tz


**! Tz**扩展显示指定的电源热量区域结构。

```dbgcmd
!tz [Address]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
要显示的电源热区的地址。 如果省略此参数, 则显示内容将包括目标计算机上的所有热区域。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要查看系统的电源功能, 请使用[ **! pocaps**](-pocaps.md) extension 命令。 若要查看系统的电源策略, 请使用[ **! popolicy**](-popolicy.md) extension 命令。 有关电源功能和电源策略的信息, 请参阅 Windows 驱动程序工具包 (WDK) 文档和*Microsoft Windows 内部机制*, 标记 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

若要随时停止执行, 请按 CTRL + BREAK (在 WinDbg 中) 或按 CTRL + C (在 KD 中)。

 

 





