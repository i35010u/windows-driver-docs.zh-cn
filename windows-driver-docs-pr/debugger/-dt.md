---
title: dt
description: Dt 扩展显示有关 CSR 线程的信息。不应将此扩展命令与 dt (显示类型) 命令混淆。
keywords:
- dt Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8c3e9a45f22a0e08960ff2edf79adfb2877c5cd8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813347"
---
# <a name="dt"></a>!dt


**！ Dt** 扩展显示有关 CSR 线程的信息。

不应将此扩展命令与 [**dt (显示类型)**](dt--display-type-.md) 命令混淆。

```dbgcmd
!dt [v] CSR-Thread 
```

## <a name="span-idddk__dt_dbgspanspan-idddk__dt_dbgspanparameters"></a><span id="ddk__dt_dbg"></span><span id="DDK__DT_DBG"></span>参数


<span id="_______v______"></span><span id="_______V______"></span>**v**   
详细模式。

<span id="_______CSR-Thread______"></span><span id="_______csr-thread______"></span><span id="_______CSR-THREAD______"></span>*CSR-线程*   
指定 CSR 线程的十六进制地址。

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

此扩展显示与 CSR 线程关联的 "线程"、"进程"、"客户端 ID"、"标志" 和 "引用计数"。 如果选择了详细模式，则显示还将包括列表指针、线程句柄和等待块。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**!dp (!ntsdexts.dp)**](-dp---ntsdexts-dp-.md)

 

 






