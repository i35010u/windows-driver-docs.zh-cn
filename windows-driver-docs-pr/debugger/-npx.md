---
title: npx
description: Npx 扩展显示浮点寄存器保存区的内容。
keywords:
- 注册，浮点数注册保存区域
- npx Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- npx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 47421c353b6e6104455bdce47ba23ea3d19b72f8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803303"
---
# <a name="npx"></a>!npx


**！ Npx** extension 显示浮点寄存器保存区的内容。

```dbgcmd
!npx Address
```

## <a name="span-idddk__npx_dbgspanspan-idddk__npx_dbgspanparameters"></a><span id="ddk__npx_dbg"></span><span id="DDK__NPX_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定浮动 \_ 保存区域结构的十六进制地址 \_ 。

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

 

此扩展命令只能与基于 x86 的目标计算机一起使用。

 

 





