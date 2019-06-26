---
title: 获取和释放语义
description: 获取和释放语义
ms.assetid: a0852881-c33f-427a-be8a-5b9edac81f9a
keywords:
- 同步 WDK 内核获取语义
- 同步 WDK 内核，释放语义
- 获取语义 WDK 内核
- 发布语义 WDK 内核
- 语义 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: df00cf901bb64b0406ab6b658d08b8627b261238
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387018"
---
# <a name="acquire-and-release-semantics"></a>获取和释放语义





某个操作具有*获取语义*如果其他处理器将始终看到它之前任何后续操作的效果的效果。 某个操作具有*发布语义*如果其他处理器将查看之前操作本身的影响的每个上述操作的效果。

请考虑下面的代码示例：

```cpp
 a++;
 b++;
 c++;
```

从另一个处理器的角度来看，上述操作会显示用于任何顺序出现。 例如，其他处理器可能会看到的增量`b`之前的增量`a`。

原子操作，例如， **Interlocked * Xxx*** 例程执行、 具有同时获取和发布语义，默认情况下。 但是，用于基于 Itanium 处理器执行具有只获取，或仅比的同时具有更快地释放语义的操作。 因此，系统提供了**Interlocked*Xxx*Acquire**并**Interlocked*Xxx*版本**版本的一些**Interlocked * Xxx*** 例程。

例如， [ **InterlockedIncrementAcquire** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85))例程使用获取语义来增加一个变量。 如果你已重新编写前面的代码示例，如下所示：

```cpp
 InterlockedIncrementAcquire(&a);
 b++;
 c++;
```

其他处理器将始终看到的增量`a`之前的增量`b`和`c`。

同样， [ **InterlockedIncrementRelease** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85))例程使用 release 语义来增加一个变量。 如果你已重新编写的代码示例再一次，按如下所示：

```cpp
 a++;
 b++;
 InterlockedIncrementRelease(&c);
```

其他处理器将始终查看的增量`a`并`b`之前的增量`c`。

如果处理器不提供仅有的说明获取，或仅发布语义，则系统将使用提供两种类型的语义的相应例程。 例如，在 x86 处理器这两个**InterlockedIncrementAcquire**并**InterlockedIncrementRelease**等效于**InterlockedIncrement**。

下表列出了有仅获取和仅限版本的不同版本的例程。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>互锁<em>Xxx</em>例程</th>
<th>获取语义-仅版本</th>
<th>仅发布语义版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedincrement" data-raw-source="[&lt;strong&gt;InterlockedIncrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedincrement)"><strong>InterlockedIncrement</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedIncrementAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85))"><strong>InterlockedIncrementAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedIncrementRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85))"><strong>InterlockedIncrementRelease</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockeddecrement" data-raw-source="[&lt;strong&gt;InterlockedDecrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockeddecrement)"><strong>InterlockedDecrement</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547875(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedDecrementAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547875(v=vs.85))"><strong>InterlockedDecrementAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547883(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedDecrementRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547883(v=vs.85))"><strong>InterlockedDecrementRelease</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedcompareexchange" data-raw-source="[&lt;strong&gt;InterlockedCompareExchange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-interlockedcompareexchange)"><strong>InterlockedCompareExchange</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547857(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedCompareExchangeAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547857(v=vs.85))"><strong>InterlockedCompareExchangeAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547867(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedCompareExchangeRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547867(v=vs.85))"><strong>InterlockedCompareExchangeRelease</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




