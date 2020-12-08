---
title: 'dp ( ntsdexts) '
description: Ntsdexts.dll 中的 dp 扩展显示 CSR 过程。
keywords:
- dp ( ntsdexts) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dp ( ntsdexts.dp)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d025fb77d0075e9de95c00fd3fb4a7620893e3b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805863"
---
# <a name="dp-ntsdextsdp"></a>!dp (!ntsdexts.dp)


Ntsdexts.dll 中的 **！ dp** 扩展显示 CSR 过程。

不应将此扩展命令与 [**dp (显示内存)**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) 命令，也不应与 [**！ kdext extension \***](-db---dc---dd---dp---dq---du---dw.md) 命令混淆。

```dbgcmd
!dp [v] [ PID | CSR-Process ]
```

## <a name="span-idddk__ntsdexts_dp_dbgspanspan-idddk__ntsdexts_dp_dbgspanparameters"></a><span id="ddk__ntsdexts_dp_dbg"></span><span id="DDK__NTSDEXTS_DP_DBG"></span>参数


<span id="_______v______"></span><span id="_______V______"></span>**v**   
详细模式。 使显示包含 "结构" 和 "线程列表"。

<span id="_______PID______"></span><span id="_______pid______"></span>*PID*   
指定 CSR 进程的进程 ID。

<span id="_______CSR-Process______"></span><span id="_______csr-process______"></span><span id="_______CSR-PROCESS______"></span>*CSR-进程*   
指定 CSR 进程的十六进制地址。

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
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此扩展显示进程地址、进程 ID、序列号、标志和引用计数。 如果选择 "详细" 模式，则会显示更多详细信息，并显示每个进程的线程信息。

如果未指定进程，则显示所有进程。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**!dt**](-dt.md)

 

 






