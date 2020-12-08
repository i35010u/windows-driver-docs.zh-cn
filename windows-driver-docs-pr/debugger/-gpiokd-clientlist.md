---
title: gpiokd.clientlist
description: Gpiokd. clientlist 命令显示所有已注册的 GPIO 控制器。
keywords:
- gpiokd clientlist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.clientlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2e2a23499819ab5aa5790acbb77130c586f04a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824759"
---
# <a name="gpiokdclientlist"></a>!gpiokd.clientlist


**！ Clientlist** 命令显示所有已注册的 GPIO 控制器 gpiokd。

```dbgcmd
!gpiokd.clientlist [Flags] 
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
用于指定显示哪些信息的标志。 此参数是以下一个或多个标志的按位 "或"。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="0x1"></span><span id="0X1"></span>0x1</p></td>
<td align="left"><p>对于每个控制器，将显示详细信息，包括其所有银行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>如果设置了位 0 (0x1) 并设置了此标志 (0x2) ，则会显示每个银行的启用和屏蔽寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x4"></span><span id="0X4"></span>0x4</p></td>
<td align="left"><p>如果设置了位 0 (0x1) 并且已设置了此标志 (0x4) ，则显示内容包括未配置的 pin。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Gpiokd.dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[GPIO 扩展](gpio-extensions.md)

 

 






