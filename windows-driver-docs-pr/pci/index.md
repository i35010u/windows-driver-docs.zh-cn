---
title: PCI 驱动程序编程指南
description: PCI 驱动程序编程指南
ms.assetid: 014f6243-6166-42e1-9f0f-1a438c77fd78
keywords:
- PCI WDK 总线
- 总线 WDK，PCI
- 外设组件互连 WDK 总线
- PCI 本地总线规范 WDK
- 配置空间 WDK PCI
- 特定于设备的配置空间 WDK PCI
- 请求配置空间信息 WDK PCI
- 电源管理 WDK PCI
- 查询电源管理功能数据
- 标题 WDK PCI
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: dde045c85fac221b0118cae05046ab40d99b0443
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "68473514"
---
# <a name="pci-driver-programming-guide"></a>PCI 驱动程序编程指南

下表汇总了不同版本的 Windows 支持的 PCIe 功能。 有关详细信息，请参阅[官方 PCIe 规范](http://pcisig.com/specifications/review-zone)中的指定部分。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>最大 Windows 版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>大小可调整的栏功能</p>
<p>请参阅 7.22 部分。</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>原子操作</p>
<p>请参阅 6.15 部分。</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="odd">
<td><p>用于优化 FW 延迟的 ACPI 添加件</p>
<p>请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkId=787058" data-raw-source="[ACPI Additions for FW Latency Optimizations]( https://go.microsoft.com/fwlink/p/?LinkId=787058)">用于优化 FW 延迟的 ACPI 添加件</a></p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>ATS/PRI</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=787061" data-raw-source="[ATS specification](https://go.microsoft.com/fwlink/p/?LinkId=787061)">ATS 规范</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=787060" data-raw-source="[Errata for the PCI Express&#174; Base Specification Revision 3.1, Single Root I/O Virtualization and Sharing Revision 1.1, Address Translation and Sharing Revision 1.1, and M.2 Specification Revision 1.0](https://go.microsoft.com/fwlink/p/?LinkId=787060)">PCI Express® 基础规范修订版 3.1、单根 I/O 虚拟化和共享修订版 1.1、地址转换和共享修订版 1.1 和 M.2 规范修订版 1.0 的勘误表</a></li>
</ul></td>
<td><p>Windows 10</p></td>
</tr><td><p>优化的缓冲区刷新/填充 (OBFF)</p>
<p>请参阅 6.19 部分。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
<tr class="even">
<td><p>延迟容限报告 (LTR) 功能</p>
<p>请参阅 7.25 部分。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>替代路由 ID 解释 (ARI)</p>
<p>请参阅 6.13 部分。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
<tr class="even">
<td><p>消息信号中断 (MSI/MSI-X) 支持</p>
<p>请参阅 6.1.4 部分。</p></td>
<td><p>Windows Vista</p>
<p>Windows Server 2008 R2</p></td>
</tr>
<tr class="odd">
<td><p>TLP 处理提示 (TPH)</p>
<p>请参阅 6.17 部分。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
<tr class="even">
<td><p>单根 I/O 虚拟化 (SR-IOV)</p>
<p>请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-" data-raw-source="[Single Root I/O Virtualization (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)">单根 I/O 虚拟化 (SR-IOV)</a>。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
</tbody>
</table>

## <a name="in-this-section"></a>本部分内容

- [PCI 电源管理和设备驱动程序](https://docs.microsoft.com/windows-hardware/drivers/pci/pci-power-management-and-device-drivers)
- [访问 PCI 设备配置空间](https://docs.microsoft.com/windows-hardware/drivers/pci/accessing-pci-device-configuration-space)
- [减少 I/O 资源使用](https://docs.microsoft.com/windows-hardware/drivers/pci/i-o-resource-usage-reduction)
- [启动设备 IRP 中的资源顺序](https://docs.microsoft.com/windows-hardware/drivers/pci/order-of-resources-in-start-device-irp)
- [有关图形的 PCI Express 常见问题解答](https://docs.microsoft.com/windows-hardware/drivers/pci/pci-express-faq-for-graphics)
- [PCI 示例](https://docs.microsoft.com/windows-hardware/drivers/pci/pci-sample)

## <a name="see-also"></a>另请参阅

- [官方 PCIe 规范](http://pcisig.com/specifications/review-zone)
