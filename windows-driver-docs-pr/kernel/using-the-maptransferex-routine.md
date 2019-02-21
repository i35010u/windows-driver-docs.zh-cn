---
title: 使用 MapTransferEx 例程
description: MapTransferEx 例程初始化一系列以前分配的 DMA 资源并开始 DMA 传输。
ms.assetid: 79D3DDB2-B134-43B2-A6CC-94035C793047
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c72ea9dd940cee71186c0b829bc536cf74143aed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541055"
---
# <a name="using-the-maptransferex-routine"></a>使用 MapTransferEx 例程


[ **MapTransferEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406521)例程初始化一系列以前分配的 DMA 资源并将开始 DMA 传输。 DMA 操作接口的版本 3 中提供了此例程。 从 Windows 8 开始支持此接口的版本 3。 有关 DMA 操作接口的详细信息，请参阅[ **DMA\_OPERATIONS**](https://msdn.microsoft.com/library/windows/hardware/ff544071)。

## <a name="comparison-of-maptransferex-to-maptransfer"></a>到 MapTransfer MapTransferEx 的比较


**MapTransferEx**是的改进的版本[ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)例程。 **MapTransfer** DMA 操作接口，从 Windows 2000 中的版本 1 开始的所有版本中可用。 调用一次**MapTransfer**可以将映射从 MDL 的物理内存的一个连续的块。 但是，可能会由 MDL 链描述复杂 DMA 传输的数据缓冲区，链中的每个 MDL 可能描述多个物理上连续内存块。 若要使用**MapTransfer**传输此类缓冲区，驱动程序必须对多次调用**MapTransfer**。 通常，在一对嵌套循环内进行这些调用。 内部循环从一个连续内存块的物理访问在每个 MDL 和外部循环进行循环访问从一个 MDL 到 MDL 链中下一步。

与此相反，一个调用到**MapTransferEx**可以针对复杂的 DMA 传输传输整个数据缓冲区。 以下三种**MapTransferEx**参数描述要用于传输的缓冲区内存。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>Mdl</em></td>
<td><p>指向一个或多个 MDLs 链中的第一个 MDL 的指针。 有关 MDL 链的详细信息，请参阅<a href="using-mdls.md" data-raw-source="[Using MDLs](using-mdls.md)">使用 MDLs</a>。</p></td>
</tr>
<tr class="even">
<td><em>Offset</em></td>
<td><p>从开始按 MDL 供应链所述的内存缓冲区的字节偏移量。</p></td>
</tr>
<tr class="odd">
<td><em>长度</em></td>
<td><p>指向包含数据缓冲区的长度，以字节为单位的位置的指针。</p></td>
</tr>
</tbody>
</table>

 

在开头**MapTransferEx**调用，请**MapTransferEx**例程可进入 MDL 链以查找的缓冲区开始。 指定的缓冲区开始*偏移量*参数。 下一步，从开始的缓冲区开始到结束时，工作**MapTransferEx**构造散播-聚集列表中的每个缓冲区列表中的片段是物理上连续 MDL 链中的内存块。 若要构造此列表中， **MapTransferEx**步骤从一个物理上连续中每个 MDL 下, 一步的内存块和一个 MDL MDL 链中下一步。 列表构造已完成时通过散播-聚集列表所述的缓冲区内存的总量等于指定的字节数\**长度*输入的参数。 在结果列表中分散/聚拢缓冲区片段的顺序匹配 MDL 链中的物理上连续块的顺序。

## <a name="multiple-calls-to-maptransferex"></a>多次调用 MapTransferEx


**MapTransferEx**可能始终无法传输一次调用中的整个 DMA 数据缓冲区。 以下列表介绍了一些可能需要的条件**MapTransferEx**不止一次调用以完成传输：

-   DMA 适配器要求映射寄存器和的映射寄存器分配给适配器的数量不足以描述整个缓冲区。
-   分配的驱动程序，以便包含散播-聚集列表存储不足够大以包含整个缓冲区的分散/集中列表。
-   传输使用系统 DMA 控制器，用于限制可以在硬件散播-聚集列表中指定的缓冲区片段数。

在这些情况下，所有**MapTransferEx**映射尽可能多的数据缓冲区，可使用一次调用，并指示驱动程序通过调用映射缓冲区的大小。 前面的列表不包含其他条件，例如，可能需要多个调用的特定于平台缓存行为**MapTransferEx**完成传送。 将来的硬件平台可能会施加其他 DMA 传输长度约束。 出于这些原因，驱动程序开发人员应该设计其驱动程序来正确处理这种情况在其**MapTransferEx**无法映射一次调用中的整个 DMA 数据缓冲区。

然后再调用**MapTransferEx**，调用方集\**长度*参数中仍需要映射的 DMA 数据缓冲区的字节数。 在返回之前， **MapTransferEx**设置\**长度*到缓冲区中实际已映射的调用的字节数。 当**MapTransferEx**调用不能将整个缓冲区长度，指定的映射\**长度*输入的值、 的输出值\**长度*小于其输入值。 如果 DMA 传输需要两个或更多**MapTransferEx**调用，调用驱动程序必须获得\**长度*之前可以指定输出值从一次调用\* *长度*输入值以用于下一次调用。

例如，如果**MapTransferEx**调用可以传输仅 X 到或从其缓冲区字节*偏移量*= B 和\**长度*= N （上输入），然后，在返回时，\**长度*= X。为下一步调用**MapTransferEx**，该驱动程序应设置*偏移量*= B + X 并\**长度*= N-X。在这两个调用中，无需修改即可使用相同的 MDL 链。

如果调用方指定[ *DmaCompletionRoutine*](https://msdn.microsoft.com/library/windows/hardware/hh450991)， **MapTransferEx**写入\**长度*输出之前的值它会安排*DmaCompletionRoutine*运行。 此行为可确保已更新\**长度*值始终是可用之前*DmaCompletionRoutine*运行。 例如，如果 DMA 传输需要两个**MapTransferEx**调用， *DmaCompletionRoutine*第一个调用的计划可以获取\**长度*从第一次调用的输出值。 例程然后可以使用此值来计算\**长度*输入值以用于第二次调用。 通常情况下，*长度*参数指向的位置\* *CompletionContext*值提供给*DmaCompletionRoutine*为参数。

 

 




