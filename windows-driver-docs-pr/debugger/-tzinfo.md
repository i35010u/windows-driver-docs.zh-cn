---
title: tzinfo
description: Tzinfo 扩展显示指定热量区域信息结构的内容。
ms.assetid: a30826d8-b7c5-4fbc-a3c3-b7a994eaf7fe
keywords:
- 热量区域信息
- tzinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tzinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6af9551157a543c2fe8dc5b51aa53e38a876e481
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025155"
---
# <a name="tzinfo"></a>!tzinfo


**! Tzinfo**扩展显示指定热量区域信息结构的内容。

```dbgcmd
!tzinfo Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
要显示的热区域信息结构的地址。

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

 

 





