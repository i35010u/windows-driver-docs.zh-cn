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
ms.openlocfilehash: 369da6be516d4686dc1d3694b4d7653c2d0e566c
ms.sourcegitcommit: 403dbca9d5d8f092d6a06edeb21bf887445ccf35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59540501"
---
# <a name="bug-check-0xff-reservequeueoverflow"></a>Bug 检查 0xFF：RESERVE\_QUEUE\_OVERFLOW


预留\_队列\_溢出错误检查的值为 0x000000FF。 这表示尝试保留队列，从而导致溢出的队列中插入新项。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


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

## <a name="resolution"></a>分辨率 
[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。
 

 




