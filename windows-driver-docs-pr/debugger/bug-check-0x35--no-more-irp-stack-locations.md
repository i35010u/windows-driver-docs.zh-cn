---
title: Bug 检查 0x35 NO_MORE_IRP_STACK_LOCATIONS
description: NO_MORE_IRP_STACK_LOCATIONS bug 检查的值为0x00000035。 此 bug 检查在 IoCallDriver 数据包没有更多堆栈位置的情况下发生。
keywords:
- Bug 检查 0x35 NO_MORE_IRP_STACK_LOCATIONS
- NO_MORE_IRP_STACK_LOCATIONS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NO_MORE_IRP_STACK_LOCATIONS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f395375b918e88f5153ae8cb9431386da80db38f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830281"
---
# <a name="bug-check-0x35-no_more_irp_stack_locations"></a>Bug 检查0x35：不再 \_ 有 \_ IRP \_ 堆栈 \_ 位置


"不再 \_ 更多 \_ IRP \_ 堆栈 \_ 位置 bug 检查" 的值为 "0x00000035"。 此 bug 检查在 **IoCallDriver** 数据包没有更多堆栈位置的情况下发生。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="no_more_irp_stack_locations-parameters"></a>无 \_ 更多 \_ IRP \_ 堆栈 \_ 位置参数


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
<td align="left"><p>IRP 的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

较高级别的驱动程序已尝试通过 **IoCallDriver** 接口调用较低级别的驱动程序，但数据包中没有更多的堆栈位置。 这会阻止低级驱动程序访问其参数。

这是一种灾难性的情况，因为更高级别的驱动程序将继续执行，就像它已根据需要) 为低级驱动程序 (填写参数一样。 但是，由于后一驱动程序没有堆栈位置，因此，前者实际上写出了数据包的末尾。 这意味着其他一些内存也已损坏。

 

 




