---
title: 池分配和免费例程
description: 池分配和免费例程
ms.assetid: 757eebc0-ebd4-49a1-acea-6c27956b4b23
keywords:
- RDBSS WDK 文件系统中，池分配
- 重定向驱动器缓冲子系统 WDK 文件系统中，池分配
- 池分配 WDK RDBSS
- RDBSS WDK 的文件系统，免费例程
- 重定向驱动器缓冲子系统 WDK 的文件系统，免费例程
- 免费例程 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1abe38b4e02dbaabd26b858824ad8332fa8e7d7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352912"
---
# <a name="pool-allocation-and-free-routines"></a>池分配和免费例程


## <span id="ddk_pool_allocation_and_free_functions_if"></span><span id="DDK_POOL_ALLOCATION_AND_FREE_FUNCTIONS_IF"></span>


RDBSS 提供大量例程用于池分配。 通常情况下，不是通过直接调用这些例程使用宏，调用这些例程。 宏自动处理零售版和已检查生成之间的差异。

已检验版本已设计这些例程在正常内核分配和可用例程周围添加包装。 这些包装器的池分配和可用例程提供其他调试信息并调用的例程的执行各种检查和监视在调用内核池分配和免费的例程之前的一组。 但是，这些功能当前未实现这些分配和免费的例程中，可能会添加在将来的版本。

免费版本，这些例程会变得直接调用内核分配和免费的例程[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)并[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590).

下表列出了 RDBSS 池分配和免费的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557355" data-raw-source="[&lt;strong&gt;_RxAllocatePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557355)"><strong>_RxAllocatePoolWithTag</strong></a></p></td>
<td align="left"><p>此例程会具有四个字节标记可帮助捕获内存问题的块的开头的池将分配内存。</p>
<p>建议<strong>RxAllocatePoolWithTag</strong>宏调用而不是直接使用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557358" data-raw-source="[&lt;strong&gt;_RxCheckMemoryBlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557358)"><strong>_RxCheckMemoryBlock</strong></a></p></td>
<td align="left"><p>此例程将检查的特殊 RX_POOL_HEADER 标头签名的内存块。 请注意，网络微型重定向程序驱动程序将需要此特殊的签名块添加到内存分配才能使用该例程。</p>
<p>由于尚未实现此特殊的标头块，则不应使用此例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557363" data-raw-source="[&lt;strong&gt;_RxFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557363)"><strong>_RxFreePool</strong></a></p></td>
<td align="left"><p>此例程将释放内存池。</p>
<p>建议<strong>RxFreePool</strong>宏调用而不是直接使用此例程。</p></td>
</tr>
</tbody>
</table>

 

数中定义的宏*ntrxdef.h*标头文件中，调用这些例程。 而不是调用直接在上表中列出的例程，通常使用以下宏。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxAllocatePoolWithTag</strong> (<em>type</em>, <em>size</em>, <em>tag</em>)</p></td>
<td align="left"><p>在 checked 版本中，此宏从具有四个字节标记可帮助捕获实例的内存移入垃圾桶块的开始处的池分配内存。</p>
<p>在零售版本中，此宏将成为直接调用<strong>ExAllocatePoolWithTag</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxCheckMemoryBlock</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>在 checked 版本中，此宏会检查特殊的 RX_POOL_HEADER 标头签名的内存块。</p>
<p>在零售版本，此宏没有任何影响。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxFreePool</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>在 checked 版本中，此宏可释放的内存池。</p>
<p>在零售版本中，此宏将成为直接调用<strong>ExFreePool</strong>。</p></td>
</tr>
</tbody>
</table>

 

 

 




