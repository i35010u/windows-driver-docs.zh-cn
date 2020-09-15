---
title: SerCx2 串行控制器驱动程序设计
description: 若要管理串行控制器，请编写一个串行控制器驱动程序，用于执行特定于硬件的任务并与 SerCx2 通信。
ms.assetid: 67045E19-4EE1-4C31-A842-858E9A90233E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31edb40128c008dea50f16048a352802508e4385
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103128"
---
# <a name="serial-controller-driver-design-for-sercx2"></a>SerCx2 串行控制器驱动程序设计

若要管理串行控制器，请编写一个串行控制器驱动程序，用于执行特定于硬件的任务并与 SerCx2 通信。 从 Windows 8.1 开始，SerCx2 是系统提供的组件，用于处理串行控制器常见的许多处理任务。 这些任务包括管理串行控制器客户端发送的超时和处理读取和写入请求。

## <a name="in-this-section"></a>在本节中

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="features-of-sercx2-based-serial-controller-drivers.md" data-raw-source="[Features of SerCx2-Based Serial Controller Drivers](features-of-sercx2-based-serial-controller-drivers.md)">基于 SerCx2 的串行控制器驱动程序的功能</a></p></td>
<td><p>基于 SerCx2 的串行控制器驱动程序是一种 KMDF 驱动程序，它使用 KMDF 中的方法和回调执行一般的驱动程序操作，并与 SerCx2 通信以执行特定于串行控制器驱动程序的操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="sercx2-i-o-transactions.md" data-raw-source="[SerCx2 I/O Transactions](sercx2-i-o-transactions.md)">SerCx2 I/O 事务</a></p></td>
<td><p>SerCx2 简化了读取 (的处理 <a href="/previous-versions/ff546883(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](/previous-versions/ff546883(v=vs.85))"><strong>IRP_MJ_READ</strong></a>) 并 (<a href="/previous-versions/ff546904(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](/previous-versions/ff546904(v=vs.85))"><strong>IRP_MJ_WRITE</strong></a> 串行控制器驱动程序的) 请求。 为了响应读取或写入请求，SerCx2 向串行控制器驱动程序发出一个或多个 i/o 事务。 从驱动程序的角度来看，每个事务都是一个简单且完整的 i/o 操作。</p></td>
</tr>
</tbody>
</table>