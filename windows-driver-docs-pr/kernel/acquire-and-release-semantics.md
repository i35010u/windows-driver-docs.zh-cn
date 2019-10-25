---
title: 获取和释放语义
description: 获取和释放语义
ms.assetid: a0852881-c33f-427a-be8a-5b9edac81f9a
keywords:
- 同步 WDK 内核，获取语义
- 同步 WDK 内核，发布语义
- 获取语义 WDK 内核
- 发布语义 WDK 内核
- 语义 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaccf7b1968ea5bd4f639b8117c26f61bbf739e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837286"
---
# <a name="acquire-and-release-semantics"></a>获取和释放语义





如果其他处理器在后续操作生效之前始终会看到其效果，则操作具有*获取语义*。 如果其他处理器会在操作本身的影响之前看到上述每个操作的效果，则操作具有*发布语义*。

请考虑以下代码示例：

```cpp
 a++;
 b++;
 c++;
```

从另一个处理器的角度来看，上述操作可能以任意顺序出现。 例如，另一个处理器可能会在 `a`增量之前查看 `b` 的增量。

默认情况下，原子操作（如**联锁 * Xxx*** 例程执行的操作）具有获取和释放语义。 但是，基于 Itanium 的处理器执行只获取或仅具有发布语义的操作比同时具有这两种语义的操作更快。 因此，系统为某些**联锁 * xxx*** 例程提供**互锁*Xxx*获取**和**互锁发布**版本。

例如， [**InterlockedIncrementAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85))例程使用获取语义来递增变量。 如果重写前面的代码示例，请执行以下操作：

```cpp
 InterlockedIncrementAcquire(&a);
 b++;
 c++;
```

其他处理器始终会在 `b` 和 `c`增量之前看到 `a` 的增量。

同样， [**InterlockedIncrementRelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85))例程使用 release 语义来递增变量。 如果再次重写代码示例，如下所示：

```cpp
 a++;
 b++;
 InterlockedIncrementRelease(&c);
```

其他处理器将始终在 `c`增量之前查看 `a` 和 `b` 的增量。

如果处理器未提供仅获取或仅发布语义的指令，则系统将使用提供这两种类型语义的相应例程。 例如，x86 处理器上的**InterlockedIncrementAcquire**和**InterlockedIncrementRelease**等效于**InterlockedIncrement**。

下表列出了具有仅获取和只可释放变量的例程。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>联锁<em>Xxx</em>例程</th>
<th>获取-仅语义版本</th>
<th>发布-仅语义版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement" data-raw-source="[&lt;strong&gt;InterlockedIncrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)"><strong>InterlockedIncrement</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedIncrementAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547916(v=vs.85))"><strong>InterlockedIncrementAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedIncrementRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547919(v=vs.85))"><strong>InterlockedIncrementRelease</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement" data-raw-source="[&lt;strong&gt;InterlockedDecrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement)"><strong>InterlockedDecrement</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547875(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedDecrementAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547875(v=vs.85))"><strong>InterlockedDecrementAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547883(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedDecrementRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547883(v=vs.85))"><strong>InterlockedDecrementRelease</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedcompareexchange" data-raw-source="[&lt;strong&gt;InterlockedCompareExchange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedcompareexchange)"><strong>InterlockedCompareExchange</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547857(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedCompareExchangeAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547857(v=vs.85))"><strong>InterlockedCompareExchangeAcquire</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547867(v=vs.85)" data-raw-source="[&lt;strong&gt;InterlockedCompareExchangeRelease&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff547867(v=vs.85))"><strong>InterlockedCompareExchangeRelease</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




