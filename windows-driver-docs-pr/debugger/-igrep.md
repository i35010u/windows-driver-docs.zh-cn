---
title: igrep
description: Igrep 扩展在反汇编中搜索模式。
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
ms.openlocfilehash: 4405a9f396e28932dafec304b41a2beed879047c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826953"
---
# <a name="igrep"></a>!igrep


**！ Igrep** extension 在反汇编中搜索模式。

```dbgcmd
!igrep [Pattern [StartAddress]] 
```

## <a name="span-idddk__igrep_dbgspanspan-idddk__igrep_dbgspanparameters"></a><span id="ddk__igrep_dbg"></span><span id="DDK__IGREP_DBG"></span>参数


<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*模式*   
指定要搜索的模式。 如果省略，则使用最后一种 *模式* 。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
指定从其开始搜索的十六进制地址。 如果省略，则使用当前程序计数器。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

 

 





