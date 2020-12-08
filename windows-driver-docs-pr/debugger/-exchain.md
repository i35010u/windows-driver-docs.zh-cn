---
title: exchain
description: Exchain 扩展显示当前异常处理程序链。
keywords:
- exchain Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- exchain
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 02de31094a7d14e24d16d6f03fff614ab5de94c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820417"
---
# <a name="exchain"></a>!exchain


**！ Exchain** 扩展显示当前异常处理程序链。

```dbgcmd
!exchain [Options]
```

## <a name="span-idddk__exchain_dbgspanspan-idddk__exchain_dbgspanparameters"></a><span id="ddk__exchain_dbg"></span><span id="DDK__EXCHAIN_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下值之一：

<span id="_c"></span><span id="_C"></span>**/c**  
**try** / 如果检测到此类异常，则显示与调试 c + + try **catch** 异常相关的信息。

<span id="_C"></span><span id="_c"></span>**/C**  
显示与调试 c + + **try** / **catch** 异常相关的信息，即使未检测到这样的异常也是如此。

<span id="_f"></span><span id="_F"></span>**/f**  
显示通过遍历 CRT 函数表获取的信息，即使未检测到 CRT 异常处理程序也是如此。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

**！ Exchain** 扩展仅适用于基于 x86 的目标计算机。

<a name="remarks"></a>备注
-------

**！ Exchain** 扩展显示当前线程的异常处理程序的列表。

此列表以链上第一个处理程序开始， (第一个处理程序处理异常) 并继续到末尾。 下面的示例演示了此扩展。

```dbgcmd
0:000> !exchain
0012fea8: Prymes!_except_handler3+0 (00407604)
  CRT scope  0, filter: Prymes!dzExcepError+e6 (00401576)
                func:   Prymes!dzExcepError+ec (0040157c)
0012ffb0: Prymes!_except_handler3+0 (00407604)
  CRT scope  0, filter: Prymes!mainCRTStartup+f8 (004021b8)
                func:   Prymes!mainCRTStartup+113 (004021d3)
0012ffe0: KERNEL32!GetThreadContext+1c (77ea1856)
```

 

 





