---
title: 有关图形的 PCI Express 常见问题解答
description: 本白皮书提供有关 PCI Express 图形信息对于 Microsoft Windows 操作系统，并解答常见问题。
ms.assetid: 30FC1CF9-B642-4E00-869C-63009BA3F128
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6ea7095ea2ea4c7eaf24a9afe5a85cc22a106e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353547"
---
# <a name="pci-express-faq-for-graphics"></a>有关图形的 PCI Express 常见问题解答


**上次更新时间：**

-   2004 年 6 月 30日日
-   已存档的纸。 有关技术准确性方面的内容的 url 不由不作任何担保。

**适用于：**

-   Microsoft Windows Vista
-   Microsoft Windows Server 2003
-   Microsoft Windows XP
-   Microsoft Windows 2000

本白皮书提供有关 PCI Express 图形信息对于 Microsoft Windows 操作系统，并解答常见问题。

**PCI Express**

PCI Express (PCIe) 是一种 I/O 总线技术，旨在替换外围组件互连 (PCI)、 PCI 的 X 和加速图形端口 (AGP)。 通过提供高级的功能和更高的带宽，PCIe 解决很多 PCI、 X PCI 和 AGP 的不足之处。 PCIe 保留与 PCI 本地总线规范 2.3 的完整软件兼容性和它将替换序列，点对点连接总线体系结构的 PCI 和 PCI X 并行 multidrop 总线体系结构。

由链接连接两个 PCIe 设备，每个链接由一个或多个通道组成。 每个通道包含两个低压差异信号对按相反方向携带 2.5 Gbps 流量。 有一对用于传输，另一个对用于接收。 若要进一步提高链接的带宽，多个通道可放在两个 PCIe 设备来聚合每个单独的球道的带宽之间并行 （x1，x2，x4、 x8、 x12、 x16 或 x32 通道）。

PCIe 硬件是与 Microsoft Windows 2000 和 Microsoft Windows XP 操作系统上的 PCI 软件向后兼容。 高级的 PCIe 仅在 Windows Vista 和更高版本的 Windows 中以本机方式支持功能。

**定义**

-   XPDM:Windows XP 显示器驱动程序模型。

-   WDDM:Windows Vista 显示器驱动程序模型。 WDDM 图形驱动程序基础结构了重大改进，与 XPDM 驱动程序向后兼容。

-   GART:图形地址重定位表，显示适配器提供线性化视图的非线性内存的硬件。

-   DCT:显示兼容性测试。 视频驱动程序需要通过这些测试，以符合 Windows 认证计划和由 Microsoft 进行数字签名。

-   WHQL:Windows 硬件质量实验室。 负责，Windows 硬件认证计划的 Microsoft 内部组织。

 

**PCI Express 图形**

它是已知图形可以始终使用比提供的更多带宽。 图形数据传输导致 PCI 总线上的最大的流量。 图形需求和复杂性的不断增加最终所做的 PCI 总线不足，导致 AGP 一起开发。 现在我们正在推送的 AGP 可以提供的限制，我们需要更好的解决方案。 PCIe 超出 AGP 带宽可用性，与在不久的将来扩展的更多空间。 通过增加的通道中链接数量，图形适配器可以充分利用更高的带宽和加速数据传输。 例如，使用 X16 的图形适配器链接在每个方向都有 4 Gbps 的带宽。

给定 PCIe 提供更高的带宽，系统也已转向离开 AGP PCIe。 通常情况下，系统不提供 AGP 和 PCIe 连接器。

**在 Vista 中 PCI Express 图形**

Windows Vista 显示器驱动程序模型 (WDDM) 具有针对 PCIe 图形适配器，例如，由 GPU 支持的 64 位寻址模式的特定要求。 但是，必须实现一个最少为 40 位的物理地址位。 未实现的位应强制为零。 这些要求不是适用于 Windows XP 显示器驱动程序模型。

**PCIe 图形和 AGP**

除了上面提到的带宽注意事项，还有几个其他区别 AGP 和 PCIe 之间。

根据定义，AGP 需要图形地址重定位表 (GART) 提供了到图形设备的非线性的系统内存的线性视图使用了芯片集。 PCIe，但是，需要图形设备本身而不是芯片集上存在内存线性化硬件。 因此，针对内存中 PCIe 的线性化驱动程序支持必须存在于视频驱动程序，而不是作为 AGP 样式单独 GART 微型端口驱动程序。 图形硬件供应商想要在其 Windows XP 驱动程序模型 (XPDM) 驱动程序中使用非本地的视频内存必须实现内存线性化硬件和相应的软件。 与 WDDM 兼容的所有 PCIe 图形适配器必须都支持硬件和软件中的内存线性化。

AGP 专用于图形适配器，并不使用它的任何其他设备类别。 PCIe 旨在由所有以前使用过 PCI 的设备类别。 与 AGP，大量的视频驱动程序已直接编程芯片组，它产生了严重的不良影响，例如图形堆栈中的崩溃和内存损坏。 由于在系统中，将对所有设备使用 PCIe，因此是更为重要的视频驱动程序不程序芯片集直接。

 

**常见问题**

**将在 Windows XP 上运行 PCIe 视频卡？**

是。 PCIe 是符合 PCI 的软件。 PCIe 硬件适用于支持 PCI 的操作系统。

**PCIe 图形是否共存 AGP？**

某些芯片集支持 AGP 和 X16 PCIe。 某些母板具有 AGP 和 X16 PCIe 槽使用这种芯片集。

**多监视器配置将在 PCIe 图形工作？**

多监视器配置的 PCIe 需要工作方式一样 PCI。 它们执行的操作是否取决于主板制造商。 例如，x16、 x8 和 x8 带来三倍的监视器配置将需要一个 x16 和两个 x8 槽母板上的存在。

**使用 PCIe 图形的性能问题有哪些？**

高速 PCIe 图形解决方案都具有比 AGP 更好的性能。 通常情况下，PCIe 图形卡使用 x16 PCIe 槽。 这将转化为 4 Gbps 的带宽。 这是对 AGP 8 X 的已有两重增加。 在这种情况下，"x1"意味着的槽具有一个 PCIe 球道，将为其提供 264 Mbps 的带宽。 这是等于提供的 AGP 1 倍和两次的 PCI 的带宽 (132 Mbps)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>PCIe 版本</strong></td>
<td><strong>AGP</strong></td>
<td><strong>Bandwidth</strong></td>
</tr>
<tr class="even">
<td><p>PCIe x1</p></td>
<td><p>AGP 1X</p></td>
<td><p>264 Mbps</p></td>
</tr>
<tr class="odd">
<td><p>PCIe x4</p></td>
<td><p>AGP 4X</p></td>
<td><p>1 Gbps</p></td>
</tr>
<tr class="even">
<td><p>PCIe x8</p></td>
<td><p>AGP 8X</p></td>
<td><p>2 Gbps</p></td>
</tr>
<tr class="odd">
<td><p>PCIe x16</p></td>
<td><p>2 x AGP 8X</p></td>
<td><p>4 Gbps</p></td>
</tr>
</tbody>
</table>

 

此外，AGP 规范不支持"搜寻。" 这意味着，设备需要用来映射内存非缓存写入由处理器组合以防止处理器缓存的内存或，否则昂贵的缓存刷新需要完成之间切换的 CPU 和 GPU 间的表面。 因此，该内存到处理器读取访问将会非常缓慢。

PCIe 将支持搜寻。 它将现在可将映射为可缓存此类共享的内存，并仍将能够维护 CPU 和 GPU 之间的一致性。 Snooped 的事务慢于 nonsnooped 事务，但其不利的一面由于 CPU 可以读取的共享的内存以全速，我们不需要刷新所有缓存，可能意味着在某些情况下更好的性能。

**是 n 球道 PCIe 槽兼容使用 p-球道 PCIe 图形卡，其中 p &gt; n？其中 n &gt; p？**

不能插入 x16 到 x8 图形卡插槽。 您可以但是，如果你想插入 x8 卡 PCIe 智能卡插入 x16 槽。 P 球道 PCIe 卡将一些速度的 n 球道 PCIe 槽，以在工作，其中 n &gt; p。 这不是 true，如果 n &lt; p。

## <a name="related-topics"></a>相关主题
[PCI-SIG](http://pcisig.com/)  



