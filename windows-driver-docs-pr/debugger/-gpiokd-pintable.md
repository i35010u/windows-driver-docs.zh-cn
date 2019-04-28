---
title: gpiokd.pintable
description: Gpiokd.pintable 命令显示有关数组的 GPIO 插针的信息。
ms.assetid: CBBC9BC7-D1BF-44C2-836B-703F5384D690
keywords:
- gpiokd.pintable Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.pintable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97a7b399f83e38a338d98fbfefb6e1988cd68bb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336546"
---
# <a name="gpiokdpintable"></a>!gpiokd.pintable


**！ Gpiokd.pintable**命令显示有关数组的 GPIO 插针的信息。

```dbgcmd
!gpiokd.pintable PinBase PinCount [Flags]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PinBase______"></span><span id="_______pinbase______"></span><span id="_______PINBASE______"></span> *PinBase*   
地址的数组[ \_GPIO\_PIN\_信息\_条目](gpio-extensions.md#data-structures-used-by-the-gpio-commands)结构。

<span id="_______PinCount______"></span><span id="_______pincount______"></span><span id="_______PINCOUNT______"></span> *PinCount*   
若要显示的 pin 数。

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
<td align="left"><p>不使用此命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>不使用此命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x4"></span><span id="0X4"></span>0x4</p></td>
<td align="left"><p>显示内容包括未配置的 pin。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Gpiokd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[GPIO 扩展](gpio-extensions.md)

 

 






