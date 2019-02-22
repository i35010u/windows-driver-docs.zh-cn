---
title: dt
description: Dt 扩展显示有关 CSR 线程的信息。此扩展命令不应使用 dt （显示类型） 命令混淆。
ms.assetid: 7fbca028-8d11-42b5-b64e-41eb3edc56cc
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
ms.openlocfilehash: 3c806aa1c3f1bca241c2db492a1d02c8ec15cea5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545997"
---
# <a name="dt"></a>!dt


**！ Dt**扩展显示有关 CSR 线程的信息。

不要将此扩展命令与相混淆[ **dt （显示类型）** ](dt--display-type-.md)命令。

```dbgcmd
!dt [v] CSR-Thread 
```

## <a name="span-idddkdtdbgspanspan-idddkdtdbgspanparameters"></a><span id="ddk__dt_dbg"></span><span id="DDK__DT_DBG"></span>参数


<span id="_______v______"></span><span id="_______V______"></span> **v**   
详细模式。

<span id="_______CSR-Thread______"></span><span id="_______csr-thread______"></span><span id="_______CSR-THREAD______"></span> *CSR-Thread*   
指定十六进制 CSR 线程的地址。

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

此扩展显示线程、 进程、 客户端 ID、 标志以及与 CSR 线程关联的引用计数。 如果选择详细模式，则显示还将包括列表指针、 线程句柄和等待块。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!dp (!ntsdexts.dp)**](-dp---ntsdexts-dp-.md)

 

 






