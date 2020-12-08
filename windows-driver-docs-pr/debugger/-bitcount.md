---
title: bitcount
description: ！ Bitcount extension 计算内存范围中 "1" 位的数量。
keywords:
- bitcount Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bitcount
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 845bea90a62e69aa7380b2588d7e2817aea84746
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799981"
---
# <a name="bitcount"></a>!bitcount


**！ Bitcount** extension 计算内存范围中 "1" 位的数量。

```dbgcmd
!bitcount StartAddress TotalBits
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定将对其 "1" 位进行计数的内存范围的起始地址。

<span id="_______TotalBits______"></span><span id="_______totalbits______"></span><span id="_______TOTALBITS______"></span>*TotalBits*   
指定内存范围的大小，以位为单位。

<span id="_______-_______"></span> **-?**   
在 [调试器命令窗口](debugger-command-window.md)中显示此扩展的一些帮助文本。

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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

 

 





