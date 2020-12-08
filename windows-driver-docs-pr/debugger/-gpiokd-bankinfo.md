---
title: gpiokd.bankinfo
description: Gpiokd. bankinfo 命令显示有关 GPIO bank 的信息。
keywords:
- gpiokd bankinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.bankinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 03344e07332b2bd46fe9f6f823138f6719a7497b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824765"
---
# <a name="gpiokdbankinfo"></a>!gpiokd.bankinfo


**！ Gpiokd. bankinfo** 命令显示有关 GPIO bank 的信息。

```dbgcmd
!gpiokd.bankinfo BankAddress [Flags]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______BankAddress______"></span><span id="_______bankaddress______"></span><span id="_______BANKADDRESS______"></span>*BankAddress*   
用于表示 GPIO 控制器银行的[ \_ gpio \_ BANK \_ 条目](gpio-extensions.md#data-structures-used-by-the-gpio-commands)结构的地址。

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
<td align="left"><p>显示固定表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>显示启用和屏蔽寄存器。</p></td>
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

 

 






