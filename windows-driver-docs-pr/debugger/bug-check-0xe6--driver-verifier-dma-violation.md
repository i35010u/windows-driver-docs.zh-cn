---
title: Bug 检查 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
description: DRIVER_VERIFIER_DMA_VIOLATION bug 检查具有 0x000000E6 值。 这是 bug 检查代码的所有驱动程序验证工具 DMA 验证冲突。
ms.assetid: badf8948-356c-4728-b34e-02f1638630a6
keywords:
- Bug 检查 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
- DRIVER_VERIFIER_DMA_VIOLATION
ms.date: 03/14/2019
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DMA_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4e340b024b80a29c65c4e2a25ed3f75bb4c0e3ba
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136112"
---
# <a name="bug-check-0xe6-driververifierdmaviolation"></a>Bug 检查 0xE6：驱动程序\_VERIFIER\_DMA\_冲突


该驱动程序\_VERIFIER\_DMA\_冲突错误检查的值为 0x000000E6。 这是所有驱动程序验证程序的 bug 检查代码**DMA 验证**冲突。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="driververifierdmaviolation-parameters"></a>驱动程序\_VERIFIER\_DMA\_冲突参数


参数 1 是感兴趣的唯一参数。 此参数标识的确切的冲突。 如果附加一个调试器，在调试器中显示信息性消息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">错误和调试程序消息的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00</p></td>
<td align="left"><p>此代码可表示两种类型的错误：</p>
<p>1. 该驱动程序已尝试将刷新到映射注册文件的末尾的字节数太多。 显示允许的字节数和尝试的字节数。</p>
<p>2. Windows 已用完连续映射寄存器。 显示的所需的映射寄存器的数量和最大块的连续映射寄存器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>性能计数器已减少。 显示计数器的新旧值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p>性能计数器的增加速度过快。 在调试器中显示的计数器值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>该驱动程序释放过多的 DMA 常用缓冲区。 通常这意味着它释放同一缓冲区两次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>该驱动程序释放过多 DMA 适配器通道。 通常这意味着它释放同一个适配器通道两次。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p>该驱动程序释放过多 DMA 映射寄存器。 通常这意味着它释放同一个映射寄存器两次。 显示的活动映射寄存器的数量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>该驱动程序释放 DMA 散播-聚集列表太多。 通常这意味着它释放相同散播-聚集列表两次。 显示已分配列表的数目和释放列表的数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>该驱动程序尝试释放适配器，而不首先释放其所有常见的缓冲区。 显示适配器地址和剩余的缓冲区数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>该驱动程序尝试释放适配器，而不首先释放所有适配器通道，常见的缓冲区或分散/集中列表。 显示适配器地址和剩余项的数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>该驱动程序尝试释放适配器，而不首先释放所有映射寄存器。 显示适配器地址和的剩余映射寄存器的数量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>该驱动程序尝试释放适配器，而不首先释放其所有分散/集中列表。 显示适配器地址和剩余散播-聚集列表的数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>HV_TOO_MANY_ADAPTER_CHANNELSThe 驱动程序已在同一时间分配过多适配器通道。 . （只有一个适配器通道允许每个适配器中）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>该驱动程序尝试在同一时间分配过多映射寄存器。 显示请求的数目和允许的数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>该驱动程序未刷新其适配器缓冲区。 显示驱动程序尝试将映射的字节数和最大允许字节数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>该驱动程序尝试 DMA 传输，而无需锁定缓冲区。 有问题的缓冲区是分页的内存中。 显示 MDL 的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>该驱动程序或硬件编写了其已分配的 DMA 缓冲区之外。 显示错误 （溢出或不足） 的性质，以及相关地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>尝试以释放其映射的驱动程序注册时一些仍已映射。 显示的地图寄存器仍然映射的数量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x11</p></td>
<td align="left"><p>该驱动程序有太多的适配器的未完成的引用计数。 显示引用计数和适配器地址的数量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>该驱动程序不正确的 IRQL 在调用 DMA 例程。 显示所需的 IRQL 和实际 IRQL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>该驱动程序不正确的 IRQL 在调用 DMA 例程。 显示所需的 IRQL 和实际 IRQL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>该驱动程序尝试分配过多映射寄存器。 显示请求的数目和允许的数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>该驱动程序尝试刷新未映射的缓冲区。 显示的缓冲区的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x18</p></td>
<td align="left"><p>该驱动程序已 DMA 操作尝试使用已发布，并且不再存在的适配器。 显示适配器的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x19</p></td>
<td align="left"><p>该驱动程序传递给 HAL 例程 null DMA_ADAPTER 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>该驱动程序传递给 HAL 例程的地址和 MDL。 但是，此地址不是此 MDL 边界内。 传入的地址，并显示 MDL 的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>该驱动程序尝试映射已映射的地址范围。 显示的地址范围和该范围内的当前映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>该驱动程序调用<strong>HalGetAdapter</strong>。 此函数已过时，必须使用<strong>IoGetDmaAdapter</strong>相反。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>HV_BAD_MDLThe 驱动程序引用了无效的系统地址--第一个 MDL 之前, 或之后结束，第一个 MDL，或使用的长度超过 MDL 缓冲区并跨越页边界内 MDL 的传输长度。 . 显示无效的地址和第一个 MDL 地址，或 MDL 地址和额外传输长度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>尝试刷新映射寄存器的尚未映射该驱动程序。 显示映射注册 base、 刷新地址和 MDL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>该驱动程序尝试映射传输的长度为零的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>DMA 缓冲区系统弗吉尼亚中未映射</p>
<p>参数 2-MDL</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>无法刷新尚未完成或取消的通道。 </p>
<p>2-违反行为的参数。 </p>
<p>值：0x00:非法通道刷新 </p>
<p>   参数 3 的控制器 id。</p>
<p>   参数 4-频道号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>请求的长度的缓冲区空间不足。
<p>参数 2-未占用的长度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>未知的设备说明版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>IOMMU 检测到 DMA 违反情况。 </p>
<p>参数 2 的故障设备的设备对象。</p>
<p>参数 3-在出错的信息 （通常在出错的物理地址）。</p>
<p>参数 4-错误类型 （特定于硬件）。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

请参阅每个代码的原因说明的 Parameters 节中的说明。

<a name="resolution"></a>分辨率
----------

当驱动程序验证程序已指示，若要监视一个或多个驱动程序时，才会发生此错误检查。 如果您不打算使用驱动程序验证程序，应停用它。 此外可以考虑删除驱动程序导致此问题。

如果你是驱动程序编写器，使用通过此 bug 检查获取的信息以在代码中修复的错误。

Driver Verifier **DMA 验证**选项才可用在 Windows XP 和更高版本。 有关驱动程序验证程序的完整详细信息，请参阅 Windows 驱动程序工具包。

 

 




