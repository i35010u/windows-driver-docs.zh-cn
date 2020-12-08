---
title: Bug 检查 0xF4 CRITICAL_OBJECT_TERMINATION
description: CRITICAL_OBJECT_TERMINATION bug 检查的值为0x000000F4。 这表示对系统操作至关重要的进程或线程意外退出或终止。
keywords:
- Bug 检查 0xF4 CRITICAL_OBJECT_TERMINATION
- CRITICAL_OBJECT_TERMINATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CRITICAL_OBJECT_TERMINATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d15ed1df56e57024197385991cf892c00bd03019
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805757"
---
# <a name="bug-check-0xf4-critical_object_termination"></a>Bug 检查0xF4：关键 \_ 对象 \_ 终止


"关键 \_ 对象 \_ 终止 bug 检查" 的值为 "0x000000F4"。 这表示对系统操作至关重要的进程或线程意外退出或终止。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="critical_object_termination-parameters"></a>关键 \_ 对象 \_ 终止参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>终止对象类型：</p>
<p><strong>0x3：</strong> 正在</p>
<p><strong>0x6：</strong> Thread</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>终止对象</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>进程图像文件名</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>指向包含说明性消息的 ASCII 字符串的指针</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

系统操作需要多个进程和线程。 如果出于任何原因终止，系统将无法再正常工作。

 
<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 




