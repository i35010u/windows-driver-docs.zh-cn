---
title: dp (ntsdexts.dp)
description: Ntsdexts.dll 中的分发点扩展显示 CSR 过程。
ms.assetid: 9e489cfc-2105-4605-b94d-88eea7883420
keywords:
- dp (ntsdexts.dp) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dp ( ntsdexts.dp)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0d446a9e9f0ddf20f60e73e045875c1bf1843ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336804"
---
# <a name="dp-ntsdextsdp"></a>!dp (!ntsdexts.dp)


**！ Dp** Ntsdexts.dll 中的扩展显示 CSR 过程。

不要将此扩展命令与相混淆[ **dp （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令，或与[ **！ kdext\*.dp** ](-db---dc---dd---dp---dq---du---dw.md)扩展命令。

```dbgcmd
!dp [v] [ PID | CSR-Process ]
```

## <a name="span-idddkntsdextsdpdbgspanspan-idddkntsdextsdpdbgspanparameters"></a><span id="ddk__ntsdexts_dp_dbg"></span><span id="DDK__NTSDEXTS_DP_DBG"></span>参数


<span id="_______v______"></span><span id="_______V______"></span> **v**   
详细模式。 将导致显示以包括结构和线程的列表。

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
指定 CSR 进程的进程的 ID。

<span id="_______CSR-Process______"></span><span id="_______csr-process______"></span><span id="_______CSR-PROCESS______"></span> *CSR-Process*   
指定十六进制 CSR 过程的地址。

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
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此扩展显示进程地址、 进程 ID、 序列号、 标志和引用计数。 如果选择详细模式，则显示更多详细信息，并为每个进程显示线程信息。

如果未不指定任何进程，将显示所有进程。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!dt**](-dt.md)

 

 






