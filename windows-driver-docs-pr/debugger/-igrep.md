---
title: igrep
description: Igrep 扩展搜索反汇编中的模式。
ms.assetid: f76aa84b-6d52-4b36-b2d0-d4a8d47d510e
keywords:
- igrep Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- igrep
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c3696a8748cb5b84de485d2ba700708454626b7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520431"
---
# <a name="igrep"></a>！ igrep


**！ Igrep**扩展搜索的反汇编模式。

```dbgcmd
!igrep [Pattern [StartAddress]] 
```

## <a name="span-idddkigrepdbgspanspan-idddkigrepdbgspanparameters"></a><span id="ddk__igrep_dbg"></span><span id="DDK__IGREP_DBG"></span>参数


<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *Pattern*   
指定要搜索的模式。 如果省略，上次*模式*使用。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
指定要开始搜索的十六进制地址。 如果省略，则使用当前的程序计数器。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

 

 





