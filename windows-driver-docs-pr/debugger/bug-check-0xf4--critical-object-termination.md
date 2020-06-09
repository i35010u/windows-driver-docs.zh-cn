---
title: Bug 检查 0xF4 CRITICAL_OBJECT_TERMINATION
description: CRITICAL_OBJECT_TERMINATION bug 检查的值为0x000000F4。 这表示对系统操作至关重要的进程或线程意外退出或终止。
ms.assetid: 51a73ada-5e82-45a2-ad2a-8ef53f96318c
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
ms.openlocfilehash: 2b5b38327eeede96d0e2e7cb1d579153c33ac070
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534788"
---
# <a name="bug-check-0xf4-critical_object_termination"></a>Bug 检查0xF4：关键 \_ 对象 \_ 终止


"关键 \_ 对象 \_ 终止 bug 检查" 的值为 "0x000000F4"。 这表示对系统操作至关重要的进程或线程意外退出或终止。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="critical_object_termination-parameters"></a>关键 \_ 对象 \_ 终止参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>终止对象类型：</p>
<p><strong>0x3：</strong>正在</p>
<p><strong>0x6：</strong>Thread</p></td>
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
 




