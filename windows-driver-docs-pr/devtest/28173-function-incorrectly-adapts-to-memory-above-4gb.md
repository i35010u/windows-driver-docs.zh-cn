---
title: C28173
description: 警告的 C28173 当前函数似乎错误地适应 4GB 以上的物理内存。
ms.assetid: 9332c35e-9d04-4286-9eff-3a639589607e
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28173
ms.openlocfilehash: 07d445a07d935364dc6b172a946ca38b21dbfc25
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533470"
---
# <a name="c28173"></a>C28173


警告 C28173:当前函数似乎错误地适应 4GB 以上的物理内存

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>代码似乎不从调用中恢复<strong>IoGetDmaAdapter</strong>返回映射寄存器一小部分。 请参阅文档了解详细信息。</p></td>
</tr>
</tbody>
</table>

 

在具有 4 GB 的内存，系统上**IoGetDmaAdapter**函数可能会返回更少映射寄存器比请求; 这将成为更有可能时请求的值将成为大 (接近 64)。这是因为需要将映射到 4 gb 的空间 4 GB 以上物理内存。

不会不适应代码获取比它要求更少寄存器，则会出现此警告消息。 当一个函数将调用**IoGetDmaAdapter**，代码分析工具模拟**IoGetDmaAdapter**函数返回不是请求的较小的寄存器的数量。 调用的函数必须处理这种情况，并返回成功。

请注意的是其他驱动程序可能会失败，具有 4 GB 以上的系统的方式。 应检查这些可能的故障模式的代码。 有关 4GB 内存问题和映射寄存器的详细信息，请参阅[ **NdisMAllocateMapRegisters**](https://msdn.microsoft.com/library/windows/hardware/ff552300)。

 

 





