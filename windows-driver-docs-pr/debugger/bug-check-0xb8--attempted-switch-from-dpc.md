---
title: Bug 检查 0xB8 ATTEMPTED_SWITCH_FROM_DPC
description: ATTEMPTED_SWITCH_FROM_DPC bug 检查的值为0x000000B8。 这表明延迟的过程调用 (DPC) 例程尝试执行非法操作。
keywords:
- Bug 检查 0xB8 ATTEMPTED_SWITCH_FROM_DPC
- ATTEMPTED_SWITCH_FROM_DPC
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_SWITCH_FROM_DPC
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8dd82b12e7b12a16a819854eaa1afa227fa13e1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832839"
---
# <a name="bug-check-0xb8-attempted_switch_from_dpc"></a>Bug 检查0xB8：尝试 \_ \_ 从 \_ DPC 切换


\_ \_ 从 DPC BUG 检查尝试的开关的 \_ 值为0x000000B8。 这表明延迟的过程调用 (DPC) 例程尝试执行非法操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="attempted_switch_from_dpc-parameters"></a>尝试 \_ \_ 从 \_ DPC 参数进行切换


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
<td align="left"><p>导致故障的原始线程</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>新线程</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>原始线程的堆栈地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

从 DPC 例程尝试等待操作、附加进程或收益。 这是非法操作。

<a name="resolution"></a>解决方法
----------

堆栈跟踪将导致导致错误的原始 DPC 例程中的代码。

 

 




