---
title: ioresdes
description: Ioresdes 扩展显示指定地址处的 IO_RESOURCE_DESCRIPTOR 结构。
ms.assetid: a57dd414-16d6-4515-9eee-dac91398906b
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
ms.openlocfilehash: 7fe4f2bff66961e0fe2c713c394e483e4efead11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336434"
---
# <a name="ioresdes"></a>!ioresdes


**！ Ioresdes**扩展插件都会显示 IO\_资源\_指定地址处的描述符结构。

```dbgcmd
!ioresdes Address 
```

## <a name="span-idddkioresdesdbgspanspan-idddkioresdesdbgspanparameters"></a><span id="ddk__ioresdes_dbg"></span><span id="DDK__IORESDES_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的十六进制地址的 IO\_资源\_描述符结构。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 有关 IO\_资源\_描述符结构，请参阅 Windows Driver Kit (WDK) 文档。

 

 





