---
title: 联锁操作数的驱动程序注释
description: 联锁操作数的驱动程序注释
ms.assetid: 33C85016-765B-42BF-9F38-BB682951B20C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1627979e9e575c25b3d950dfbec137c575f18e1c
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381993"
---
# <a name="driver-annotations-for-interlocked-operands"></a>联锁操作数的驱动程序注释


大型函数系列将使用联锁处理器指令访问的变量的地址作为其参数之一。 这些是缓存读取原子说明，如果未正确使用操作数，则会产生非常微妙的 bug。

使用以下函数参数批注将其标识为互锁操作数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">联锁操作数批注</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_Interlocked_operand_"></span><span id="_interlocked_operand_"></span><span id="_INTERLOCKED_OPERAND_"></span><em>Interlocked_operand</em></p></td>
<td align="left"><p>带批注的函数参数是某个联锁函数的目标操作数。 这些操作数必须具有特定的附加属性。</p></td>
</tr>
</tbody>
</table>



用互锁操作数批注的函数参数 \_ \_ \_ 应该在进程之间共享。 与此批注一起使用的变量必须：

-   声明为 **volatile。**

-   不是局部变量。 使用本地变量通常指示函数意向的误解。 即使本地变量在某种程度上是共享的，系统分页要求也会导致另一个进程出现问题。

-   除联锁函数外，不能访问。 如果没有显式使用联锁函数，该操作可能会访问陈旧的数据，可能只会出现在单个处理器的缓存中，或者可能会延迟到系统的其余部分。

系统提供的函数已在联锁操作数上进行了注释。

下面的示例显示了 [**InterlockedExchange**](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedexchange) 函数的批注。 此批注指定必须始终使用联锁操作访问目标参数。

```
LONG  
InterlockedExchange (  
    _Inout_ _Interlocked_operand_ LONG volatile *Target,  
    _In_ LONG Value  
    );  
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[用于驱动程序的 SAL 2.0 批注](sal-2-annotations-for-windows-drivers.md)