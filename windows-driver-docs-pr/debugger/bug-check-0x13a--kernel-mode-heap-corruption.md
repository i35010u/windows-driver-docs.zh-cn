---
title: Bug 检查 0x13A KERNEL_MODE_HEAP_CORRUPTION
description: KERNEL_MODE_HEAP_CORRUPTION bug 检查的值为 0x0000013A。 这表示内核模式堆管理器检测到堆中存在损坏。
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
# <a name="bug-check-0x13a-kernel_mode_heap_corruption"></a>Bug 检查 0x13A：KERNEL\_MODE\_HEAP\_CORRUPTION

KERNEL\_MODE\_HEAP\_CORRUPTION bug 检查的值为 0x0000013A。 这表示内核模式堆管理器检测到堆中存在损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="kernel_mode_heap_corruption-parameters"></a>KERNEL\_MODE\_HEAP\_CORRUPTION Parameters

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
<td align="left"><p>检测到的损坏类型 - 请参阅下面的列表</p></td>
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

### <a name="parameter-1---type-of-heap-corruption"></a>参数 1 - 堆损坏的类型

0x3：检测到损坏的条目标头。

0x4：检测到多个损坏的条目标头。

0x5：检测到大分配中的损坏条目标头。

0x6：检测到与缓冲区溢出一致的功能损坏。

0x7：检测到与缓冲区不足一致的功能损坏。

0x8：将可用块传递到仅对繁忙块有效的操作。

0x9：为当前操作指定的参数无效。

0xA：检测到无效的分配类型。

0xB：检测到与“可用后使用”错误一致的功能损坏。

0XC：为当前操作指定了错误的堆。

0xD：检测到可用列表已损坏。

0xE：堆在可用列表以外的列表中检测到列表损坏。

0xF：将可用块传递到仅对繁忙块有效的操作。

0x10：堆在当前操作期间检测到无效的内部状态。 这通常是缓冲区溢出的结果。

0x11：堆在当前操作期间检测到无效的内部状态。 这通常是缓冲区溢出的结果。

0x12：堆在当前操作期间检测到无效的内部状态。 这通常是缓冲区溢出的结果。

0x13：向堆 API 传递一个空堆句柄。 查看调用堆栈并确定为堆提供错误句柄的原因。

0x14：请求堆分配大于当前分配限制。

0x15：在执行提交请求的过程中，已确定该请求将超过当前提交限制。

0x16：在检查给定 VA 管理器分配的大小的过程中，确定查询无效。

## <a name="resolution"></a>分辨率

[!analyze](-analyze.md) 调试扩展显示有关 bug 检查的信息，并有助于确定根本原因  。

[!heap](-heap.md) 扩展显示堆使用信息、控制堆管理器中的断点、检测泄漏的堆块、搜索堆块或显示页堆信息。
