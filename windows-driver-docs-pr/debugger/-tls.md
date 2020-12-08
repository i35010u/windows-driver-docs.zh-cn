---
title: tls
description: Tls 扩展显示 (TLS) 槽的线程本地存储。
keywords:
- TLS（线程本地存储）
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
ms.openlocfilehash: 48298d791ef1116f198b985a9d8ab93fd447e710
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803287"
---
# <a name="tls"></a>!tls


**！ Tls** 扩展显示 (tls) 槽的线程本地存储。

```dbgcmd
!tls Slot [TEB]
```

## <a name="span-idddk__tls_dbgspanspan-idddk__tls_dbgspanparameters"></a><span id="ddk__tls_dbg"></span><span id="DDK__TLS_DBG"></span>参数


<span id="_______Slot______"></span><span id="_______slot______"></span><span id="_______SLOT______"></span>*槽*   
指定 TLS 槽。 该值可以是0到1088之间的任何值 (decimal) 。 如果 *槽* 为-1，则显示所有槽。

<span id="_______TEB______"></span><span id="_______teb______"></span>*TEB*   
指定线程环境块 (TEB) 。 如果此为0或省略，则使用当前线程。

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

 

<a name="remarks"></a>备注
-------

以下是示例：

```dbgcmd
0:000> !tls -1
TLS slots on thread: c08.f54
0x0000 : 00000000
0x0001 : 003967b8
0:000> !tls 0
c08.f54: 00000000
```

 

 





