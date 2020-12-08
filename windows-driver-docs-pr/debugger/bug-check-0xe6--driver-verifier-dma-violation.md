---
title: Bug 检查 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
description: DRIVER_VERIFIER_DMA_VIOLATION bug 检查的值为0x000000E6。 这是所有驱动程序验证程序 DMA 验证冲突的 bug 检查代码。
keywords:
- Bug 检查 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
- DRIVER_VERIFIER_DMA_VIOLATION
ms.date: 05/07/2019
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DMA_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22477f83e8adfac46febc860d044be3ee7eec27d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841363"
---
# <a name="bug-check-0xe6-driver_verifier_dma_violation"></a>Bug 检查0xE6：驱动程序 \_ 验证程序 \_ DMA \_ 冲突


驱动程序 \_ 验证程序 \_ DMA \_ 冲突 bug 检查的值为0x000000E6。 这是所有驱动程序验证程序 **DMA 验证** 冲突的 bug 检查代码。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

> [!NOTE]
> 未启用驱动程序验证程序时，可以观察到 E6 的主要错误检查代码。 如果你遇到此代码，但未启用驱动程序验证程序，请参阅 [DMA 验证](../devtest/dma-verification.md) 页。 

## <a name="driver_verifier_dma_violation-parameters"></a>驱动程序 \_ 验证程序 \_ DMA \_ 冲突参数


参数1是感兴趣的唯一参数。 此参数标识完全冲突。 如果附加了调试器，则调试器中将显示一条信息性消息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">错误和调试器消息的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00-杂项 DMA 错误。</p></td>
<td align="left"><p>此代码可以表示参数2所示的两种错误：</p>
<p>0x1-驱动程序尝试将太多字节刷新到地图注册文件的结尾。 
<p>参数 3-MDL 中剩余的字节数。</p>
<p>参数 4-请求刷新的字节数。</p>
<p>0x2-Windows 已用尽了连续的映射寄存器。 </p>
<p>参数 3-需要映射寄存器。</p>
<p>参数 4-连续映射寄存器的数目。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>性能计数器已减少。 将显示计数器的新旧值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p>性能计数器的增长速度太快。 计数器值显示在调试器中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>驱动程序释放了太多 DMA 公用缓冲区。 通常，这意味着它将两次释放相同的缓冲区。 </p>
<p>参数 2-已释放的额外常见缓冲区数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>驱动程序释放了太多 DMA 适配器通道。 通常，这意味着它将同一适配器通道释放两次。</p>
<p> 参数 2-释放的额外适配器通道数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p>驱动程序释放了太多 DMA 映射寄存器。 通常，这意味着它释放了两次相同的映射寄存器。 </p>
<p>参数 2-释放的额外映射寄存器的数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>驱动程序释放了太多 DMA 散播/聚集列表。 通常，这意味着它释放了两次相同的分散/收集列表。</p>
<p>参数 2-分配的分散集合列表。 </p>
<p>参数 3-释放的散播-聚集列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>驱动程序在没有首先释放其所有公用缓冲区的情况下尝试发布适配器。 </p>
<p> 参数 2-指向 DMA 适配器的指针。</p>
<p> 参数 3-未完成的常见缓冲区数。</p>
<p> 参数 4-指向相应内部验证程序数据的指针。 </p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>该驱动程序尝试释放适配器，而无需首先释放所有适配器通道、公用缓冲区或分散/收集列表。 <p> <p> 参数 2-指向 DMA 适配器的指针。
<p> 参数 3-未完成的适配器通道数。
<p> 参数 4-指向相应内部验证程序数据的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>该驱动程序在没有首先释放所有映射寄存器的情况下尝试发布适配器。</p> 
<p>参数 2-指向 DMA 适配器的指针。</p>
<p>参数 3-未完成的映射寄存器的数目。</p>
<p>参数 4-指向相应内部验证程序数据的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>该驱动程序尝试释放适配器，而不首先释放其所有散播/聚集列表。 </p>
<p>参数 2-指向 DMA 适配器的指针。</p>
<p>参数 3-未完成的分散收集列表的数目。</p>
<p>参数 4-指向相应内部验证程序数据的指针。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>驱动程序同时分配了过多的适配器通道 (每个适配器只允许一个适配器通道。 ) </p>
<p>参数 2-未完成的适配器通道。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>驱动程序尝试同时分配过多的地图寄存器。 </p>
<p>参数 2-所需的映射寄存器。</p>
<p>参数 3-最大映射寄存器。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>驱动程序未刷新其适配器缓冲区。</p>
<p>参数 2-映射的字节数。</p>
<p>参数 3-一次可以映射的最大字节数。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>驱动程序在未锁定缓冲区的情况下尝试了 DMA 传输。 相关缓冲区位于分页内存中。 </p>
<p>参数 2-DMA 缓冲区 MDL 的地址。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>驱动程序或硬件在其分配的 DMA 缓冲区之外写入。 参数2是冲突代码。</p>

<p>0x01：已修改 DMA 缓冲区之前的标记。需要标记为 DmaVrfy0。</p>
<p>参数 3-缓冲区长度。</p>
<p>参数 4-启动缓冲区。</p>
<p>0x02：在 DMA 缓冲区之后修改了标记。</p>
需要标记为 DmaVrfy0。
<p>参数 3-缓冲区长度。</p>
<p>参数 4-启动缓冲区。</p>
0x03： Free map 注册已被覆盖。</p>
<p>参数 3-损坏地址。 预期的填充模式为0x0F。</p>
0x04：在未正确修改缓冲区之前填充。</p>
<p>参数 3-启动缓冲区。 预期填充为0x0F。</p>
<p>参数 4-损坏地址。</p>
0x05：缓冲区被错误修改后的填充。</p>
<p>参数 3-启动缓冲区。</p>
<p>参数 4-损坏地址。 需要填充模式为0x0F。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>驱动程序尝试释放其映射寄存器，而某些仍在进行映射。 </p>
<p>参数 2-仍在映射的寄存器的数目。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x11</p></td>
<td align="left"><p>驱动程序的适配器未完成的引用计数太多。 </p>
<p>参数 2-引用计数。</p>
<p>参数 3-指向 DMA 适配器的指针。</p>
<p>参数 4-指向相应内部验证程序数据的指针。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>驱动程序在不正确的 IRQL 处称为 DMA 例程。 参数2是冲突代码。</p>
0x01：当前 IRQL 不同于预期。
<p>参数 3-预期的 IRQL。</p>
<p>参数 4-当前 IRQL。</p>
0x02：当前 IRQL 比预期高。</p>
<p>参数 3-预期最大 IRQL。</p>
<p>参数 4-当前 IRQL。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>驱动程序在不正确的 IRQL 处称为 DMA 例程。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>驱动程序尝试分配的映射寄存器太多。</p> 
<p>参数 2-分配的映射寄存器。</p>
<p>参数 3-最大映射寄存器。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>驱动程序尝试刷新未映射的缓冲区。 </p>
<p>参数 2-映射寄存器的系统虚拟空间中的地址。</p>
<p>参数 3-指向相应内部验证程序数据的指针。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x18</p></td>
<td align="left"><p>驱动程序通过使用已发布但不再存在的适配器尝试了 DMA 操作。 </p>
<p>参数 2-指向 DMA 适配器的指针。</p>
<p>参数 3-指向相应内部验证程序数据的指针。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x19</p></td>
<td align="left"><p>驱动程序向 HAL 例程传递了 null DMA_ADAPTER 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>驱动程序将地址和 MDL 传递到 HAL 例程。 但是，此地址不在此 MDL 的边界内。 </p>
<p>参数 2-超出 MDL 界限的虚拟地址。</p>
<p>参数 3-MDL。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>驱动程序尝试映射已映射的地址范围。 </p>
<p>参数 2-要映射的开始缓冲区。 </p>
<p>参数 3-要映射的缓冲区。 </p>
<p>参数 4-缓冲区中已映射的系统地址。
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>称为 <strong>HalGetAdapter</strong>的驱动程序。 此函数已过时-必须改用 <strong>IoGetDmaAdapter</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p> DMA 缓冲区无效。 驱动程序引用了无效的系统地址--在第一个 MDL 之前，或在第一个 MDL 结束之后，或使用比 MDL 缓冲区长的传输长度，并越过 MDL 内的页面边界。参数2是冲突代码。</p>
<p>0x01：虚拟缓冲区地址位于第一个 MDL 之前。</p>
<p>参数 3-DMA 缓冲区开头的虚拟地址。</p>
<p>参数 4-指向描述 DMA 缓冲区的第一个 MDL 的指针。</p>

<p>0x02：虚拟地址在第一个 MDL 之后。</p>
<p>参数 3-DMA 缓冲区开头的虚拟地址。</p>
<p>参数 4-指向描述 DMA 缓冲区的第一个 MDL 的指针。</p>

<p>0x03：额外的传输长度跨越页面边界。</p>
<p>参数 3-指向描述 DMA 缓冲区的 MDL 的指针。</p>
<p>参数 4-DMA 传输的长度。

<p>0x04： DMA 缓冲区的虚拟地址没有缓存对齐。
<p>参数 3-DMA 缓冲区开头的虚拟地址。</p>
<p>参数 4-指向描述 DMA 缓冲区的 MDL 的指针。</p>

<p>0x05： DMA 缓冲区长度不是缓存对齐。</p>
<p>参数 3-DMA 缓冲区的长度。</p>
<p>参数 4-指向描述 DMA 缓冲区的 MDL 的指针。
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>驱动程序尝试刷新尚未映射的映射寄存器。</p>
<p>参数 2-映射寄存器基。</p>
<p>参数 3-DMA 缓冲区开头的 VA。</p>
<p>参数 4-指向用于描述 DMA 缓冲区的 MDL 的指针。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>驱动程序试图映射一个长度为零的缓冲区进行传输。</p>
<p>参数 2-指向相应内部验证程序数据的指针。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>系统 VA 中未映射 DMA 缓冲区。</p>
<p>参数 2-MDL</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>无法刷新尚未完成或取消的通道。 </p>
<p>参数 2-冲突代码。 </p>
<p>值：0x00：非法的通道刷新 </p>
<p>参数 3-控制器 Id。</p>
<p>参数 4-频道号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>请求长度的缓冲区不足。</p>
<p>参数 2-无人负责长度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>未知设备说明版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>IOMMU 检测到 DMA 冲突。 </p>
<p>参数 2-出错设备的设备对象。</p>
<p>参数 3-错误信息 (通常是错误的物理地址) 。</p>
<p>参数 4-错误类型 (硬件特定) 。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

有关原因的说明，请参阅参数部分中每个代码的说明。

<a name="resolution"></a>解决方法
----------

此 bug 检查只能在已指示驱动程序验证器监视一个或多个驱动程序时出现。 如果你不打算使用驱动程序验证程序，则应停用它。 你还可以考虑删除导致此问题的驱动程序。

如果您是驱动程序编写者，请使用通过此 bug 检查获取的信息来修复代码中的 bug。

有关驱动程序验证程序的详细信息，请参阅 [驱动程序验证](../devtest/driver-verifier.md)器。

 

