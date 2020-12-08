---
title: Bug 检查 0x13B PASSIVE_INTERRUPT_ERROR
description: PASSIVE_INTERRUPT_ERROR bug 检查的值为0x0000013B。 这表示内核检测到被动级别中断的问题。
keywords:
- Bug 检查 0x13B PASSIVE_INTERRUPT_ERROR
- PASSIVE_INTERRUPT_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PASSIVE_INTERRUPT_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 77d751ddda42b0f80f6cb540d844fffccb448f79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824321"
---
# <a name="bug-check-0x13b-passive_interrupt_error"></a>Bug 检查0x13B：被动 \_ 中断 \_ 错误


被动 \_ 中断 \_ 错误错误检查的值为0x0000013B。 这表示内核检测到被动级别中断的问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="passive_interrupt_error-parameters"></a>被动 \_ 中断 \_ 错误参数


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
<td align="left">1</td>
<td align="left"><p>检测到的错误类型</p>
0x1：驱动程序尝试获取中断旋转锁，但传入了被动级中断对象。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">被动级别中断的 KINTERRUPT 对象的地址。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">预留</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

 

 




