---
title: 禁用堆栈扩展
description: 禁用堆栈扩展
keywords:
- '禁用 (全局标志的堆栈扩展) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76a7e1aaeaf751f7409fed7aaaab2027eb42fb2c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840841"
---
# <a name="disable-stack-extension"></a>禁用堆栈扩展


## <span id="ddk_disable_stack_extension_dtools"></span><span id="DDK_DISABLE_STACK_EXTENSION_DTOOLS"></span>


**禁用堆栈扩展** 标志可防止内核将进程中的线程堆栈扩展到超出初始提交的内存。

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
<td align="left"><p>映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

此功能用于模拟内存不足的情况 (其中，堆栈扩展) 并测试预期在内存不足的情况下正常运行的战略系统进程。

 

 





