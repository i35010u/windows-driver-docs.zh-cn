---
title: tls
description: Tls 扩展显示线程本地存储 (TLS) 槽。
ms.assetid: 43325322-8e6e-47fc-b1ec-8b1c304bb1e9
keywords:
- TLS （线程本地存储区）
- 线程本地存储 (TLS)
- tls Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tls
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bac89887b4586dcee99d1bec67589a58bec0c984
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564267"
---
# <a name="tls"></a>!tls


**！ Tls**扩展显示线程本地存储 (TLS) 槽。

```dbgcmd
!tls Slot [TEB]
```

## <a name="span-idddktlsdbgspanspan-idddktlsdbgspanparameters"></a><span id="ddk__tls_dbg"></span><span id="DDK__TLS_DBG"></span>参数


<span id="_______Slot______"></span><span id="_______slot______"></span><span id="_______SLOT______"></span> *Slot*   
指定 TLS 槽。 这可以是介于 0 和 1088 （十进制） 之间的任何值。 如果*槽*为-1，将显示所有槽。

<span id="_______TEB______"></span><span id="_______teb______"></span> *TEB*   
指定的线程环境块 (TEB)。 如果这是 0 或省略，则使用当前线程。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

<a name="remarks"></a>备注
-------

下面是一个示例：

```dbgcmd
0:000> !tls -1
TLS slots on thread: c08.f54
0x0000 : 00000000
0x0001 : 003967b8
0:000> !tls 0
c08.f54: 00000000
```

 

 





