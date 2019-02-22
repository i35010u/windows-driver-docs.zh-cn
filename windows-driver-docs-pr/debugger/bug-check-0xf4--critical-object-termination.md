---
title: Bug 检查 0xF4 CRITICAL_OBJECT_TERMINATION
description: CRITICAL_OBJECT_TERMINATION bug 检查具有 0x000000F4 值。 这表示，进程或线程至关重要的系统操作已意外退出或已终止。
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
ms.openlocfilehash: 8b21b988ada0a56956a36ecce7e18d0dfb5258f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540742"
---
# <a name="bug-check-0xf4-criticalobjecttermination"></a>Bug 检查 0xF4:关键\_对象\_终止


严重\_对象\_终止 bug 检查的值为 0x000000F4。 这表示，进程或线程至关重要的系统操作已意外退出或已终止。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="criticalobjecttermination-parameters"></a>关键\_对象\_终止参数


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
<td align="left"><p>终止的对象类型：</p>
<p><strong>0x3:</strong>过程</p>
<p><strong>0x6:</strong>线程</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>正在终止对象</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>进程图像文件名称</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>包含说明性消息的 ASCII 字符串的指针</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

多个进程和线程所必需的系统的操作。 时因故被终止，系统可以不再起作用。

 
<a name="resolution"></a>分辨率
----------

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。
 




