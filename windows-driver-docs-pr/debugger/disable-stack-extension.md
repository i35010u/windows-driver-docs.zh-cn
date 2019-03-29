---
title: 禁用堆栈扩展
description: 禁用堆栈扩展
ms.assetid: e4c95103-4f98-4f79-a46c-c8040e39791b
keywords:
- 禁用堆栈扩展 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 554fac533a332b92db0c2cb62816f05a151fe00c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565570"
---
# <a name="disable-stack-extension"></a>禁用堆栈扩展


## <span id="ddk_disable_stack_extension_dtools"></span><span id="DDK_DISABLE_STACK_EXTENSION_DTOOLS"></span>


**禁用 stack 扩展**标志可防止内核扩展中的初始提交的内存之外进程的线程的堆栈。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>dse</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x10000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_DISABLE_STACK_EXTENSION</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

若要模拟内存不足的情况 （其中堆栈扩展会失败） 和测试的战略系统进程的预期也甚至使用低内存来运行使用此功能。

 

 





