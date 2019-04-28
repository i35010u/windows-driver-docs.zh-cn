---
title: gpiokd.clientlist
description: Gpiokd.clientlist 命令显示所有已注册的 GPIO 控制器。
ms.assetid: 4951C2D2-FA98-4600-A98D-1BC98080D2EB
keywords:
- gpiokd.clientlist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.clientlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1e94768331f8175c0a7cf425aa782d384e0d3e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336551"
---
# <a name="gpiokdclientlist"></a>!gpiokd.clientlist


**！ Gpiokd.clientlist**命令显示所有已注册的 GPIO 控制器。

```dbgcmd
!gpiokd.clientlist [Flags] 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定所显示的信息的标志。 此参数是一个或多个下列标志的按位 OR。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="0x1"></span><span id="0X1"></span>0x1</p></td>
<td align="left"><p>对于每个控制器中，将显示详细的信息，包括所有其银行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>如果位 0 (0x1) 设置，而设置此标志 (0x2)，将显示每个单元的启用和掩码寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x4"></span><span id="0X4"></span>0x4</p></td>
<td align="left"><p>如果位 0 (0x1) 设置并设置此标志 (0x4)，显示内容包括未配置的 pin。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Gpiokd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[GPIO 扩展](gpio-extensions.md)

 

 






