---
title: gpiokd.bankinfo
description: Gpiokd.bankinfo 命令显示有关 GPIO 银行信息。
ms.assetid: C4AFF469-0624-4D59-AE78-9D7FC407AC3A
keywords:
- gpiokd.bankinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.bankinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b6f8f2ec0ac79179f8b44c926a8234dbaf50920
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568185"
---
# <a name="gpiokdbankinfo"></a>!gpiokd.bankinfo


**！ Gpiokd.bankinfo**命令显示有关 GPIO 银行信息。

```dbgcmd
!gpiokd.bankinfo BankAddress [Flags]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______BankAddress______"></span><span id="_______bankaddress______"></span><span id="_______BANKADDRESS______"></span> *BankAddress*   
地址[ \_GPIO\_银行\_条目](gpio-extensions.md#data-structures-used-by-the-gpio-commands)结构，它表示为 GPIO 控制器的插槽。

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
<td align="left"><p>显示 pin 表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>显示启用和掩码寄存器信息。</p></td>
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

 

 






