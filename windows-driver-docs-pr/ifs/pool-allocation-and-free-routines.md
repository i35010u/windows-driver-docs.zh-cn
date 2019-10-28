---
title: 池分配和免费例程
description: 池分配和免费例程
ms.assetid: 757eebc0-ebd4-49a1-acea-6c27956b4b23
keywords:
- RDBSS WDK 文件系统，池分配
- 重定向驱动器缓冲子系统 WDK 文件系统，池分配
- 池分配 WDK RDBSS
- RDBSS WDK 文件系统，免费例程
- 重定向驱动器缓冲子系统 WDK 文件系统，免费例程
- 免费例程 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c5f018913de323fd05a5f26660b52792c80bc53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841031"
---
# <a name="pool-allocation-and-free-routines"></a>池分配和免费例程


## <span id="ddk_pool_allocation_and_free_functions_if"></span><span id="DDK_POOL_ALLOCATION_AND_FREE_FUNCTIONS_IF"></span>


RDBSS 提供了许多用于池分配的例程。 通常，使用宏调用这些例程，而不是直接调用这些例程。 宏会自动处理零售版本和已检查版本之间的差异。

在已检查的版本上，这些例程旨在围绕普通内核分配和自由例程添加包装。 这些包装用于池分配和自由例程提供额外的调试信息，并调用一组在调用内核池分配和自由例程之前执行各种检查和保护的例程。 不过，这些功能当前在这些分配和免费例程中未实现，但可能会在将来的版本中添加。

在免费版本上，这些例程会直接调用内核分配和自由例程[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)和[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)。

下表列出了 RDBSS 池分配和自由例程。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxallocatepoolwithtag" data-raw-source="[&lt;strong&gt;_RxAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxallocatepoolwithtag)"><strong>_RxAllocatePoolWithTag</strong></a></p></td>
<td align="left"><p>此例程使用块开头的包含四个字节的标记从池中分配内存，有助于捕获内存问题。</p>
<p>建议调用<strong>RxAllocatePoolWithTag</strong>宏，而不是直接使用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock" data-raw-source="[&lt;strong&gt;_RxCheckMemoryBlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock)"><strong>_RxCheckMemoryBlock</strong></a></p></td>
<td align="left"><p>此例程检查内存块中是否有特殊的 RX_POOL_HEADER 标头签名。 请注意，网络小型重定向器驱动程序需要将此特殊的签名块添加到分配的内存，以便使用该例程。</p>
<p>不应使用此例程，因为尚未实现此特殊标头块。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool" data-raw-source="[&lt;strong&gt;_RxFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool)"><strong>_RxFreePool</strong></a></p></td>
<td align="left"><p>此例程释放内存池。</p>
<p>建议调用<strong>RxFreePool</strong>宏，而不是直接使用此例程。</p></td>
</tr>
</tbody>
</table>

 

*Ntrxdef*头文件中定义了许多宏，它们调用这些例程。 通常使用以下宏，而不是直接调用上表中列出的例程。

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
<td align="left"><p><strong>RxAllocatePoolWithTag</strong> （<em>类型</em>、<em>大小</em>、<em>标记</em>）</p></td>
<td align="left"><p>在选中的生成上，此宏从池中分配包含四个字节标记的池中的内存，这可以帮助捕获内存 trashing 的实例。</p>
<p>在零售版上，此宏会直接调用<strong>ExAllocatePoolWithTag</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxCheckMemoryBlock</strong> （<em>ptr</em>）</p></td>
<td align="left"><p>在选中的生成上，此宏会检查内存块中是否有特殊的 RX_POOL_HEADER 标头签名。</p>
<p>在零售版上，此宏不执行任何操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxFreePool</strong> （<em>ptr</em>）</p></td>
<td align="left"><p>在选中的生成上，此宏释放内存池。</p>
<p>在零售版上，此宏会直接调用<strong>ExFreePool</strong>。</p></td>
</tr>
</tbody>
</table>

 

 

 




