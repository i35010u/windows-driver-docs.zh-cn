---
title: Bug 检查 0x13A KERNEL_MODE_HEAP_CORRUPTION
description: KERNEL_MODE_HEAP_CORRUPTION bug 检查的值为0x0000013A。 这表示内核模式堆管理器检测到堆中的损坏。
ms.assetid: 806669B3-B811-462A-A3B6-2F583BF0E19A
keywords:
- Bug 检查 0x13A KERNEL_MODE_HEAP_CORRUPTION
- KERNEL_MODE_HEAP_CORRUPTION
ms.date: 02/14/2020
topic_type:
- apiref
api_name:
- KERNEL_MODE_HEAP_CORRUPTION
api_type:
- NA
ms.localizationpriority: high
ms.openlocfilehash: 986f5e5684c586579ca6766c8b114eae58affac0
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402351"
---
# <a name="bug-check-0x13a-kernel_mode_heap_corruption"></a>Bug 检查0x13A：内核\_模式\_堆\_损坏

内核\_模式\_堆\_损坏 bug 检查的值为0x0000013A。 这表示内核模式堆管理器检测到堆中的损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="kernel_mode_heap_corruption-parameters"></a>内核\_模式\_堆\_损坏参数

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
<td align="left">1</td>
<td align="left"><p>检测到的损坏类型-请参阅下面的列表</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">报告损坏的堆的地址</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">检测到损坏的地址</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

### <a name="parameter-1---type-of-heap-corruption"></a>参数 1-堆损坏的类型

0x3：检测到损坏的条目标头。

0x4：检测到多个损坏的条目标头。

0x5：检测到大分配中的损坏条目标头。

0x6：检测到损坏的功能与缓冲区溢出的功能一致。

0x7：检测到损坏，其中的功能与缓冲区不足。

0x8：将一个免费块传递到仅对繁忙块有效的操作。

0x9：为当前操作指定了无效的参数。

0xA：检测到无效的分配类型。

0xB：检测到具有与使用后使用错误一致的功能的损坏。

0xC：为当前操作指定了错误的堆。

0xD：检测到已损坏的可用列表。

0xE：堆检测到列表损坏列表，而不是可用列表。

0xF：将一个免费块传递到仅对繁忙块有效的操作。

0x10：堆在当前操作过程中检测到无效的内部状态。 这通常是缓冲区溢出的结果。

0x11：堆在当前操作过程中检测到无效的内部状态。 这通常是缓冲区溢出的结果。

0x12：堆在当前操作过程中检测到无效的内部状态。 这通常是缓冲区溢出的结果。

0x13：堆 API 传递了 NULL 堆句柄。 查看调用堆栈并确定为堆提供错误句柄的原因。

0x14：请求的堆分配大于当前分配的限制。

0x15：在执行提交请求的过程中，确定请求会超过当前的提交限制。

0x16：在检查给定 VA 管理器分配大小的过程中，确定查询无效。

## <a name="resolution"></a>分辨率

[ **！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

[！堆](-heap.md)扩展显示堆使用情况信息，控制堆管理器中的断点，检测泄漏的堆块，搜索堆块，或显示页堆信息。
