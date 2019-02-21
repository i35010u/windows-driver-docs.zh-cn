---
title: 互锁操作数的驱动程序批注
description: 互锁操作数的驱动程序批注
ms.assetid: 33C85016-765B-42BF-9F38-BB682951B20C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65c1f021f73da6f72fa077c8a1b79097535a9df1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542356"
---
# <a name="driver-annotations-for-interlocked-operands"></a>互锁操作数的驱动程序批注


一大系列函数将作为其参数之一应使用互锁的处理器指令进行访问的变量的地址。 这些是缓存直读原子说明，并且如果操作数使用不正确，导致非常难以发现的 bug。

使用以下函数参数的批注将其识别为主互锁操作数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">互锁的操作数批注</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_Interlocked_operand_"></span><span id="_interlocked_operand_"></span><span id="_INTERLOCKED_OPERAND_"></span><em>Interlocked_operand</em></p></td>
<td align="left"><p>带批注的函数参数是互锁函数之一的目标操作数。 这些操作数必须具有特定的附加属性。</p></td>
</tr>
</tbody>
</table>



函数参数使用批注\_Interlocked\_操作数\_需要两个进程之间共享。 必须使用与此批注的变量：

-   声明为**易失性。**

-   不是本地变量。 本地变量的用途通常表示函数的意图的误解。 即使以某种方式共享本地变量，分页的系统要求进行寻址的变量在其他进程中有问题。

-   访问除通过互锁函数。 无需显式使用互锁函数，该操作可能会访问过时的数据、 仅在单个处理器的缓存中，可能会发生或可能延迟到达系统的其余部分。

系统提供的函数已进行批注针对互锁操作数。

下面的示例演示的批注[ **InterlockedExchange** ](https://msdn.microsoft.com/library/windows/hardware/ff547892)函数。 此批注指定目标参数必须始终可通过使用互锁的操作进行访问。

```
LONG  
InterlockedExchange (  
    _Inout_ _Interlocked_operand_ LONG volatile *Target,  
    _In_ LONG Value  
    );  
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[SAL 2.0 注释驱动程序](sal-2-annotations-for-windows-drivers.md)










