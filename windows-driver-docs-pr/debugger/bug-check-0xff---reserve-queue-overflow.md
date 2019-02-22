---
title: Bug 检查 0xFF RESERVE_QUEUE_OVERFLOW
description: RESERVE_QUEUE_OVERFLOW bug 检查具有 0x000000FF 值。 这表示尝试保留队列，从而导致溢出的队列中插入新项。
ms.assetid: d327ea41-c568-49f6-8b37-183533fd6261
keywords:
- Bug 检查 0xFF RESERVE_QUEUE_OVERFLOW
- RESERVE_QUEUE_OVERFLOW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RESERVE_QUEUE_OVERFLOW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0a3b1446f96bcc99febbf39ef2b06c26ade1a715
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555215"
---
# <a name="bug-check-0xff-reservequeueoverflow"></a>Bug 检查 0xFF:RESERVE\_QUEUE\_OVERFLOW


预留\_队列\_溢出错误检查的值为 0x000000FF。 这表示尝试保留队列，从而导致溢出的队列中插入新项。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="reservequeueoverflow-parameters"></a>预留\_队列\_溢出参数


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
<td align="left"><p>保留队列的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留队列的大小</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

 

 




