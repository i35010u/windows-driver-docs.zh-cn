---
title: 使用 MapTransferEx 例程
description: MapTransferEx 例程初始化一组以前分配的 DMA 资源并启动 DMA 传输。
ms.assetid: 79D3DDB2-B134-43B2-A6CC-94035C793047
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9ded07867af93b12bbb052c69999bb1a76760c92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835847"
---
# <a name="using-the-maptransferex-routine"></a>使用 MapTransferEx 例程


[**MapTransferEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer_ex)例程初始化一组以前分配的 dma 资源并启动 dma 传输。 此例程在 DMA 操作接口版本3中可用。 从 Windows 8 开始，支持此接口的版本3。 有关 DMA 操作接口的详细信息，请参阅[**dma\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)。

## <a name="comparison-of-maptransferex-to-maptransfer"></a>MapTransferEx 与 MapTransfer 的比较


**MapTransferEx**是[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)例程的改进版本。 所有版本的 DMA 操作接口都提供**MapTransfer** ，从 Windows 2000 的版本1开始。 对**MapTransfer**的一次调用可以从 MDL 映射一个连续物理内存块。 但是，复杂 DMA 传输的数据缓冲区可能由 MDL 链描述，链中的每个 MDL 都可能描述多个物理连续内存块。 若要使用**MapTransfer**传输此类缓冲区，驱动程序必须对**MapTransfer**进行多次调用。 通常，这些调用在一对嵌套循环中进行。 内部循环从一个连续物理内存块循环访问每个 MDL 中的下一个块，外部循环从一个 MDL 循环到 MDL 链中的下一个 MDL。

与此相反，一个对**MapTransferEx**的调用可以传输整个数据缓冲区进行复杂的 DMA 传输。 以下三个**MapTransferEx**参数描述用于传输的缓冲区内存。

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
<td><p>一个指针，指向一个或多个 MDLs 链中的第一个 MDL。 有关 MDL 链的详细信息，请参阅<a href="using-mdls.md" data-raw-source="[Using MDLs](using-mdls.md)">Using MDLs</a>。</p></td>
</tr>
<tr class="even">
<td><em>抵销</em></td>
<td><p>从 MDL 链描述的内存开始的缓冲区的字节偏移量。</p></td>
</tr>
<tr class="odd">
<td><em>长度</em></td>
<td><p>指向一个位置的指针，该位置包含数据缓冲区的长度（以字节为单位）。</p></td>
</tr>
</tbody>
</table>

 

在**MapTransferEx**调用开始时， **MapTransferEx**例程会前进到 MDL 链，以查找缓冲区的起始位置。 缓冲区的开头由*Offset*参数指定。 接下来，从缓冲区开头到末尾， **MapTransferEx**将构造一个散点/集合列表，其中列表中的每个缓冲区片段都是来自 MDL 链的物理上连续的内存块。 若要构造此列表，请从一个物理上连续的内存块**MapTransferEx**到下一个 mdl 内的下一个，以及从一个 MDL 到 mdl 链中的下一个 mdl 的步骤。 当散点/集合列表描述的缓冲区内存总量等于 \**长度*输入参数指定的字节数时，将完成 List 构造。 生成的散点/集合列表中的缓冲区片段顺序与 MDL 链中物理上连续块的顺序相匹配。

## <a name="multiple-calls-to-maptransferex"></a>多个对 MapTransferEx 的调用


**MapTransferEx**可能始终无法在一个调用中传输整个 DMA 数据缓冲区。 以下列表描述了一些可能需要多次调用才能完成传输的条件**MapTransferEx** ：

-   DMA 适配器需要映射寄存器，分配给适配器的映射寄存器数不足以描述整个缓冲区。
-   驱动程序分配的包含散点/集合列表的存储空间不足，无法包含整个缓冲区的散点/集合列表。
-   传输使用系统 DMA 控制器，用于限制可在硬件散播/聚集列表中指定的缓冲区片段的数目。

在所有这些情况下， **MapTransferEx**会在一个调用中映射尽可能多的数据缓冲区，并通知驱动程序由调用映射了多少缓冲区。 前面的列表不包含其他条件（例如特定于平台的缓存行为），可能需要对**MapTransferEx**进行多次调用才能完成传输。 将来的硬件平台可能会对 DMA 传输长度施加其他约束。 由于这些原因，驱动程序开发人员应设计其驱动程序以正确处理**MapTransferEx**无法在一个调用中映射整个 DMA 数据缓冲区的情况。

在调用**MapTransferEx**之前，调用方将 \**长度*参数设置为 DMA 数据缓冲区中仍需要映射的字节数。 在返回之前， **MapTransferEx**将 \*的*长度*设置为该调用实际映射的缓冲区中的字节数。 当**MapTransferEx**调用无法映射 \**长度*输入值指定的整个缓冲区长度时，\**长度*的输出值小于其输入值。 如果 DMA 传输需要两个或多个**MapTransferEx**调用，则调用驱动程序必须从一个调用中获取 \**长度*的输出值，然后才能指定下一次调用的 \**长度*输入值。

例如，如果**MapTransferEx**调用只能向*偏移量*= B 并且 \**Length* = N （输入时）的缓冲区传输 X 个字节，则在返回时 \**Length* = X。对于下一个对**MapTransferEx**的调用，驱动程序应设置*Offset* = B + X 并且 \**Length* = N-X。在两次调用中，使用相同的 MDL 链而不进行修改。

如果调用方指定了[*DmaCompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-dma_completion_routine)，则**MapTransferEx**将在计划*DmaCompletionRoutine*运行之前写入 \**长度*的输出值。 此行为可确保在*DmaCompletionRoutine*运行之前，更新的 \**长度*值始终可用。 例如，如果 DMA 传输需要两个**MapTransferEx**调用，则第一个调用计划的*DmaCompletionRoutine*可以获取第一个调用中的 \**长度*输出值。 然后，例程可以使用此值来计算第二次调用的 \**长度*输入值。 通常，*长度*参数指向作为参数提供给*DmaCompletionRoutine*的 \**CompletionContext*值中的某个位置。

 

 




