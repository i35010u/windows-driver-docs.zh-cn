---
title: Bug 检查 0xCE DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS
description: DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS bug 检查的值为0x000000CE。 这表明驱动程序在卸载之前未能取消挂起的操作。
keywords:
- Bug 检查 0xCE DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS
- DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_UNLOADED_WITHOUT_CANCELLING_PENDING_OPERATIONS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dd2ce086c6c0e1d3eda55e5195d4ae3dc0e27965
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825205"
---
# <a name="bug-check-0xce-driver_unloaded_without_cancelling_pending_operations"></a>Bug 检查0xCE：驱动程序已 \_ 卸载， \_ 无需 \_ 取消 \_ 挂起的 \_ 操作


在 \_ \_ 未 \_ 取消 \_ 挂起操作 bug 检查的情况下卸载的驱动程序的 \_ 值为0x000000CE。 这表明驱动程序在卸载之前未能取消挂起的操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_unloaded_without_cancelling_pending_operations-parameters"></a>已卸载驱动程序， \_ \_ 但未 \_ 取消 \_ 挂起的 \_ 操作参数


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
<td align="left"><p>引用的内存地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0：</strong> 读取</p>
<p><strong>1：</strong> 写入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>引用内存的地址（如果已知）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

如果能够识别出导致错误的驱动程序，则其名称将打印在蓝屏上，并存储在内存中的 (PUNICODE\_STRING) KiBugCheckDriver  位置。

<a name="cause"></a>原因
-----

此驱动程序在卸载之前未能取消后备链表列表、Dpc、工作线程或其他此类项。

 

 




