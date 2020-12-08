---
title: ioresdes
description: Ioresdes 扩展显示指定地址处的 IO_RESOURCE_DESCRIPTOR 结构。
keywords:
- ioresdes Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ioresdes
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f5154487a570ea2837f4dbbd1294983fa0cb5796
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788947"
---
# <a name="ioresdes"></a>!ioresdes


**！ Ioresdes** extension 显示 \_ \_ 指定地址处的 IO 资源描述符结构。

```dbgcmd
!ioresdes Address 
```

## <a name="span-idddk__ioresdes_dbgspanspan-idddk__ioresdes_dbgspanparameters"></a><span id="ddk__ioresdes_dbg"></span><span id="DDK__IORESDES_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 IO \_ 资源描述符结构的十六进制地址 \_ 。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序。 有关 IO \_ 资源 \_ 描述符结构的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

 

 





