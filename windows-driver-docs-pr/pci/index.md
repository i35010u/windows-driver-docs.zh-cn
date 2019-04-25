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
ms.openlocfilehash: 180cb4ad234242d536f7124b6f84f6dcbe21c89a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391634"
---
# <a name="pci-driver-programming-guide"></a>PCI 驱动程序编程指南


## <a name="supported-pcie-features-in-windows"></a>Windows 中支持的 PCIe 功能


下表汇总了不同版本的 Windows 支持的 PCIe 功能。 有关详细信息，请参阅[官方 PCIe 规范](http://www.pcisig.com/specifications/pciexpress/review_zone/)中的指定部分。

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
<p>请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh440235" data-raw-source="[Single Root I/O Virtualization (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)">单根 I/O 虚拟化 (SR-IOV)</a>。</p></td>
<td><p>Windows 8</p>
<p>Windows Server 2012</p></td>
</tr>
</tbody>
</table>





## <a name="in-this-section"></a>本部分内容


-   [PCI 电源管理和设备驱动程序](https://msdn.microsoft.com/library/windows/hardware/dn607302)
-   [访问 PCI 设备配置空间](https://msdn.microsoft.com/library/windows/hardware/ff536890)
-   [减少 I/O 资源使用](https://msdn.microsoft.com/library/windows/hardware/ff537424)
-   [启动设备 IRP 中的资源顺序](https://msdn.microsoft.com/library/windows/hardware/ff537445)
-   [有关图形的 PCI Express 常见问题解答](https://msdn.microsoft.com/library/windows/hardware/dn653979)
-   [PCI 示例](https://msdn.microsoft.com/library/windows/hardware/hh450892)


## <a name="see-also"></a>另请参阅
-   [官方 PCIe 规范](http://www.pcisig.com/specifications/pciexpress/review_zone/)

 

 




