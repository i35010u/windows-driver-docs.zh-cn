---
title: 启用内核调试程序符号加载
description: 启用内核调试程序符号加载
keywords:
- '启用 (全局标志加载内核调试器符号) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea37107b97e2c2dd2b65eeea18f84cad6d7e2225
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795679"
---
# <a name="enable-loading-of-kernel-debugger-symbols"></a>启用内核调试程序符号加载


## <span id="ddk_enable_loading_of_kernel_debugger_symbols_dtools"></span><span id="DDK_ENABLE_LOADING_OF_KERNEL_DEBUGGER_SYMBOLS_DTOOLS"></span>


" **启用内核调试器符号加载** " 标志在下一次启动 Windows 时将内核符号加载到内核内存空间中。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>ksl</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x40000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_ENABLE_KDEBUG_SYMBOL_LOAD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

内核分析中使用内核符号，并使用高级内核调试工具。

 

 





