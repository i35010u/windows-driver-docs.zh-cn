---
title: poolval
description: Poolval 扩展会分析池页的标头, 并诊断可能的任何损坏。 此扩展仅适用于 Windows XP 及更高版本。
ms.assetid: b67ab2d4-c765-4721-81ed-c6b7c9a0ba6d
keywords:
- poolval Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- poolval
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a25bcbd1762b1c4e58defd28552c31fdc3f18a2
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025198"
---
# <a name="poolval"></a>!poolval


**! Poolval** extension 分析池页的标头, 并诊断可能的任何损坏。 此扩展仅适用于 Windows XP 及更高版本。

```dbgcmd
!poolval Address [DisplayLevel]
```

## <a name="span-idddk__poolval_dbgspanspan-idddk__poolval_dbgspanparameters"></a><span id="ddk__poolval_dbg"></span><span id="DDK__POOLVAL_DBG"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要分析其标头的池的地址。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span>*DisplayLevel*   
指定要包含在显示中的信息。 这可以是以下任一值 (默认值为零):

<span id="0"></span>0  
导致显示基本信息。

<span id="1"></span>2  
导致显示基本信息和链接的标头列表。

<span id="2"></span>pps-2  
导致显示基本信息、链接标头列表和基本标头信息。

<span id="3"></span>三维空间  
导致显示基本信息、链接标头列表和全部标头信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内存池的信息, 请参阅 Windows 驱动程序工具包 (WDK) 文档和*Microsoft Windows 内部机制*, 标记 Russinovich 和 David 所罗门群岛。

 

 





