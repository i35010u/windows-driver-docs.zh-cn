---
title: 使用串行框架扩展版本 2 (SerCx2)
description: 你可以编写一个串行控制器驱动程序，该驱动程序与串行框架扩展的版本2一起使用 (SerCx2) 来管理串行控制器。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59034fe1b32d921b2397361e3c050b0d46b9be55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811941"
---
# <a name="using-version-2-of-the-serial-framework-extension-sercx2"></a>使用串行框架扩展版本 2 (SerCx2)

你可以编写一个串行控制器驱动程序，该驱动程序与串行框架扩展的版本2一起使用 (SerCx2) 来管理串行控制器。 你还可以为连接到串行控制器（由 SerCx2 和串行控制器驱动程序）管理的端口的外围设备编写外围设备驱动程序。 此外设驱动程序使用 [串行 i/o 请求接口](serial-i-o-request-interface.md) 将数据传入和传出设备。 基于扩展的串行控制器驱动程序处理串行控制器的所有特定于硬件的任务，但使用 SerCx2 来执行许多所有串行控制器都通用的系统任务。 SerCx2 是系统提供的组件，从 Windows 8.1 开始。

**注意**  SerCx2 替换了 Windows 8 中引入的 (SerCx) 的串行 framework 扩展的版本1。 仅适用于在 Windows Windows 8.1 和更高版本中运行的新串行控制器驱动程序应编写为使用 SerCx2 DDIs 而不是 SerCx DDIs。 但是，Windows 8.1 和更高版本的 Windows 支持使用 SerCx DDI 的现有串行控制器驱动程序。

串行控制器是16550的通用异步接收器/发送器 (UART) 或兼容的设备。 有关详细信息，请参阅 [串行控制器驱动程序概述](serial-drivers-overview.md)。

## <a name="in-this-section"></a>在本节中

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="sercx2-architectural-overview.md" data-raw-source="[SerCx2 Architectural Overview](sercx2-architectural-overview.md)">SerCx2 体系结构概述</a></p></td>
<td><p>SerCx2 与串行控制器驱动程序一起工作，可在外围设备驱动程序与串行连接外围设备之间进行通信。 通常情况下，串行控制器集成到芯片 (SoC) 芯片上的系统中，以提供与 SoC 芯片外部设备不同但焊接到相同印刷电路板的外部设备的低 pin 计数通信。</p></td>
</tr>
<tr class="even">
<td><p><a href="serial-controller-driver-design-for-sercx2.md" data-raw-source="[Serial Controller Driver Design for SerCx2](serial-controller-driver-design-for-sercx2.md)">SerCx2 串行控制器驱动程序设计</a></p></td>
<td><p>若要管理串行控制器，请编写一个串行控制器驱动程序，用于执行特定于硬件的任务并与 SerCx2 通信。 从 Windows 8.1 开始，SerCx2 是系统提供的组件，用于处理串行控制器常见的许多处理任务。</p></td>
</tr>
<tr class="odd">
<td><p><a href="accessing-a-device-on-a-sercx2-managed-serial-port.md" data-raw-source="[Accessing a Device on a SerCx2-Managed Serial Port](accessing-a-device-on-a-sercx2-managed-serial-port.md)">访问 SerCx2 托管串行端口上的设备</a></p></td>
<td><p>SerCx2 和串行控制器驱动程序共同管理将设备永久连接到的串行端口。 若要访问 SerCx2 管理的串行端口上的外围设备，外围设备驱动程序会打开与串行端口的逻辑连接，并获得表示此连接的文件句柄。 然后，驱动程序使用此句柄将 i/o 请求发送到端口。</p></td>
</tr>
</tbody>
</table>
