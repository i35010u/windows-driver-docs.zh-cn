---
title: 有关图形的 PCI Express 常见问题解答
description: 本文提供了有关适用于 Microsoft Windows 操作系统的 PCI Express 图形的信息，并回答了常见问题。
ms.assetid: 30FC1CF9-B642-4E00-869C-63009BA3F128
ms.date: 06/30/2004
ms.localizationpriority: medium
ms.openlocfilehash: 0f800460783903a8e012b78731b668dd049c8e62
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902632"
---
# <a name="pci-express-faq-for-graphics"></a>有关图形的 PCI Express 常见问题解答

这是存档的纸张。 无担保，因为 Url 的货币内容的技术准确性。

**适用于：**

- Microsoft Windows Vista
- Microsoft Windows Server 2003
- Microsoft Windows XP
- Microsoft Windows 2000

本文提供了有关适用于 Microsoft Windows 操作系统的 PCI Express 图形的信息，并回答了常见问题。

## <a name="pci-express"></a>PCI Express

PCI Express (PCIe) 是一项 i/o 总线技术，旨在将外围组件互连 (PCI) 、PCI X 和加速图形端口 (AGP) 中。 通过提供高级功能和增加的带宽，PCIe 能解决 PCI、PCI-X 和 AGP 的许多缺点。 PCIe 保持与 PCI 本地总线规范2.3 的完整软件兼容性，并使用串行、点到点连接总线体系结构替换 PCI 和 PCI X 的并行 multidrop 总线体系结构。

两个 PCIe 设备通过链接进行连接，每个链接由一个或多个车道组成。 每个通道都包含两个低电压、以相反方向传输 2.5 Gbps 流量的信号。 一个对用于传输，另一个对用于接收。 为了进一步提高链接的带宽，可以在两个 PCIe 设备之间并行放置多个车道 (x1、x2、x4、x8、x12、x16 或 x32 航道) ，从而聚合每个单个通道的带宽。

PCIe 硬件向后兼容 Microsoft Windows 2000 和 Microsoft Windows XP 操作系统上的 PCI 软件。 只有 Windows Vista 和更高版本的 Windows 中的高级 PCIe 功能才是本机支持的。

## <a name="definitions"></a>定义

- XPDM： Windows XP 显示驱动程序模型。

- WDDM： Windows Vista 显示器驱动程序模型。 WDDM 是图形驱动程序基础结构的重大演变，并与 XPDM 驱动程序向后兼容。

- GART：图形地址重定位表，提供显示适配器的硬件和非线性内存的线性视图。

- DCT：显示兼容性测试。 视频驱动程序需要通过这些测试才能遵从 Windows 认证计划并由 Microsoft 进行数字签名。

- WHQL： Windows 硬件质量实验室。 Microsoft 中负责硬件的 Windows 认证计划的组织。

## <a name="pci-express-graphics"></a>PCI Express 图形

众所周知，图形始终可以使用比可用的带宽更多的带宽。 图形数据传输会导致 PCI 总线上的流量最大。 不断增加的图形需求和复杂度最终使 PCI 总线无法实现，从而导致 AGP 发明。 现在我们将推送 AGP 可提供的限制，并且我们需要更好的解决方案。 PCIe 超过了 AGP 的带宽可用性，在不久的将来有更多空间用于扩展。 通过增加链接中的车道数量，图形适配器可以利用增加的带宽和更快的数据传输。 例如，使用 X16 链接的图形适配器在每个方向上都有 4 Gbps 的带宽。

由于 PCIe 提供较高的带宽，系统已经从 AGP 移出到了 PCIe。 通常，系统并不提供 AGP 和 PCIe 连接器。

### <a name="pci-express-graphics-in-windows-vista"></a>Windows Vista 中的 PCI Express 图形

Windows Vista 显示器驱动程序模型 (WDDM) 对于 PCIe 图形适配器有特定要求，例如，GPU 支持64位寻址模式。 但是，必须实现至少40位的物理地址位。 未实现的位应强制为零。 这些要求不适用于 Windows XP 显示驱动程序模型。

### <a name="pcie-graphics--agp"></a>& AGP 的 PCIe 图形

除了上面所述的带宽注意事项外，AGP 与 PCIe 之间还有其他几个差异。

按照定义，AGP 需要一个带有图形地址重定位表 (GART) 的芯片集，该表为图形设备提供非线性系统内存的线性视图。 但是，PCIe 要求在图形设备上（而不是芯片）上存在内存 linearization 硬件。 因此，在 linearization 中对内存的驱动程序的驱动程序支持必须存在于视频驱动程序中，而不是作为 AGP 样式的单独 GART 微型端口驱动程序。 希望在其 Windows XP 驱动程序模型中使用非本地视频内存 (XPDM) 驱动程序的图形硬件供应商必须实现内存 linearization 硬件和相应软件。 与 WDDM 兼容的所有 PCIe 图形适配器都必须支持硬件和软件中的内存 linearization。

AGP 专用于图形适配器，没有其他设备类使用它。 PCIe 旨在供以前使用过 PCI 的所有设备类使用。 使用 AGP 时，许多视频驱动程序直接对芯片进行编程，这会导致严重的不良效果，如图形堆栈崩溃和内存损坏。 由于 PCIe 将用于系统中的所有设备，因此更重要的是，视频驱动程序不会直接对芯片组进行编程。

## <a name="frequently-asked-questions"></a>常见问题

**PCIe 视频卡是否适用于 Windows XP？** 是。 PCIe 与 PCI 软件兼容。 PCIe 硬件在支持 PCI 的操作系统上工作。

**PCIe 图形是否与 AGP 共存？** 某些芯片集支持 AGP 和 X16 PCIe。 某些主板有使用此类芯片组的 AGP 和 X16 PCIe 槽。

**Multimonitor 配置是否会在 PCIe 图形上工作？** PCIe 的 Multimonitor 配置应像 PCI 那样工作。 它们是否会依赖于主板制造商。 例如，x16、x8 和 x8 三次监视器配置将需要在主板上存在一个 x16 和两个 x8 槽。

**使用 PCIe 图形的性能有什么影响？** 高速 PCIe 图形解决方案比 AGP 具有更好的性能。 通常，PCIe 图形卡使用 x16 PCIe 槽。 这将转换为 4 Gbps 的带宽。 这已经是 AGP 8 的双重增加。 在这种情况下，"x1" 表示槽有一个 PCIe 通道，其带宽为 264 Mbps。 这等于 AGP 1X 提供的带宽和 PCI (132 Mbps) 的两倍。

|PCIe 版本|AGP|带宽|
|----|----|----|
|PCIe x1|AGP 1X|264 Mbps|
|PCIe x4|AGP 4X|1 Gbps|
|PCIe x8|AGP 8X|2 Gbps|
|PCIe x16|2 x AGP 8|4 Gbps|

此外，AGP 规范不支持 "侦听"。 这意味着，设备所使用的内存需要映射到未缓存或由处理器组合在一起，以防止处理器缓存该内存，或者需要在 CPU 和 GPU 之间的两个平面之间的移交之间完成昂贵的缓存刷新。 因此，处理器对该内存的读取访问将非常慢。

PCIe 将支持侦听。 现在可以将此类共享内存映射为可缓存，同时仍然能够维护 CPU 和 GPU 之间的一致性。 Snooped 事务比 nonsnooped 事务慢，但由于 CPU 可以全速读取共享内存，并且我们不需要刷新任何缓存，因此，在某些情况下，权衡可能意味着更好的性能。

**N 车道 PCIe 槽是否与 p 通道 PCIe 图形卡兼容，其中 p &gt; n？其中，n &gt; p？** 不能将 x16 图形卡插入 x8 插槽中。 不过，如果需要，可以将8个纸牌 PCIe 卡插入 x16 插槽中。 P 通道 PCIe 卡在 n 航道 PCIe 插槽（其中 n p）下将以某种速度运行 &gt; 。 如果 n p，则不是这样 &lt; 。

## <a name="related-topics"></a>相关主题

[PCI-SIG](https://pcisig.com/)  
