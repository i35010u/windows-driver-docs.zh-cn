---
title: C28173
description: 警告 C28173 当前函数似乎错误地适应 4 GB 以上的物理内存。
ms.assetid: 9332c35e-9d04-4286-9eff-3a639589607e
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28173
ms.openlocfilehash: 09848d08cd54882d8fa95247d0ac6f91dace8d3f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384841"
---
# <a name="c28173"></a>C28173


警告 C28173：当前函数似乎错误地适应大于 4 GB 的物理内存

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>此代码不会显示为从对返回少量映射寄存器的 <strong>IoGetDmaAdapter</strong> 的调用中恢复。 有关详细信息，请参阅文档。</p></td>
</tr>
</tbody>
</table>

 

在超过 4 GB 内存的系统上， **IoGetDmaAdapter** 函数可能会返回较少请求的映射寄存器;当请求的值变成大 (接近 64) 时，这会更有可能。这是因为需要将超过 4 GB 的物理内存映射到小于 4 GB 的空间。

当代码不适应获取更少的寄存器时，会出现此警告消息。 当函数调用 **IoGetDmaAdapter**时，代码分析工具将模拟 **IoGetDmaAdapter** 函数返回的寄存器数比请求的数目少。 调用函数必须处理此情况并成功返回。

请注意，对于超过 4 GB 的系统，驱动程序的其他方法可能会失败。 你应检查代码中的这些可能的失败模式。 有关 4 GB 内存问题和映射寄存器的详细信息，请参阅 [**NdisMAllocateMapRegisters**](/previous-versions/windows/hardware/network/ff552300(v=vs.85))。

 

