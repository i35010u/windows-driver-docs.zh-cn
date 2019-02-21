---
title: exchain
description: Exchain 扩展显示当前的异常处理程序链。
ms.assetid: 6e5c935b-e475-4213-83d8-94510a58fde5
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
ms.openlocfilehash: a1a820fcfb620faa1773f7aed5eddaf49da1b1aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541945"
---
# <a name="exchain"></a>！ exchain


**！ Exchain**扩展显示当前的异常处理程序链。

```dbgcmd
!exchain [Options]
```

## <a name="span-idddkexchaindbgspanspan-idddkexchaindbgspanparameters"></a><span id="ddk__exchain_dbg"></span><span id="DDK__EXCHAIN_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下值之一：

<span id="_c"></span><span id="_C"></span>**/c**  
显示用于调试 c + + 相关的信息**尝试**/**捕获**异常，如果检测到此类异常。

<span id="_C"></span><span id="_c"></span>**/C**  
显示用于调试 c + + 相关的信息**尝试**/**捕获**异常，即使此类异常未检测到。

<span id="_f"></span><span id="_F"></span>**/f**  
显示即使 CRT 异常处理程序未检测到 CRT 函数表的每个步骤获取的信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

**！ Exchain**扩展是仅适用于基于 x86 的目标计算机。

<a name="remarks"></a>备注
-------

**！ Exchain**扩展显示的当前线程的异常处理程序的列表。

列表开头链 （提供的第一个机会处理异常的那个） 上的第一个处理程序，并继续进行到末尾。 下面的示例显示了此扩展。

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

 

 





