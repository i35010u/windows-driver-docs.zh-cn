---
title: bushnd
description: Bushnd 扩展显示 HAL BUS_HANDLER 结构。
ms.assetid: dd2cb9c1-9abe-4209-a4fa-dc50965e807e
keywords:
- bushnd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bushnd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8fad94f5cbe2fa8fcabef12ef3523978b048e09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562516"
---
# <a name="bushnd"></a>!bushnd


**！ Bushnd**扩展插件都会显示 HAL 总线\_处理程序结构。

```dbgsyntax
    !bushnd [Address] 
```

## <a name="span-idddkbushnddbgspanspan-idddkbushnddbgspanparameters"></a><span id="ddk__bushnd_dbg"></span><span id="DDK__BUSHND_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的十六进制地址的 HAL 总线\_处理程序结构。 如果省略， **！ bushnd**显示的总线和处理程序的基址列表。

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

 

 

 





