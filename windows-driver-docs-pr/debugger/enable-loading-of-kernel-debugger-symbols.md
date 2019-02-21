---
title: 启用内核调试程序符号加载
description: 启用内核调试程序符号加载
ms.assetid: ce047073-9cfd-4ab2-bd58-48a2acc55351
keywords:
- 启用加载内核调试程序符号 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a59ea4dd2c1d1540302da4af371594c6faeb709
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523508"
---
# <a name="enable-loading-of-kernel-debugger-symbols"></a>启用内核调试程序符号加载


## <span id="ddk_enable_loading_of_kernel_debugger_symbols_dtools"></span><span id="DDK_ENABLE_LOADING_OF_KERNEL_DEBUGGER_SYMBOLS_DTOOLS"></span>


**启用内核调试程序符号加载**标志将内核符号加载到下一次 Windows 启动的内核内存空间。

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
<td align="left"><p>整个系统的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

内核符号用于在内核分析并通过高级的内核调试工具。

 

 





