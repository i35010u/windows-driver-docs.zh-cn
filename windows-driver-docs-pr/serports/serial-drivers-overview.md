---
title: 串行控制器驱动程序概述
description: 所有版本的 Windows 都为串行控制器设备提供驱动程序支持。
ms.assetid: 1EA0221E-0F68-429B-9DA5-4AE2D3394A09
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4ad1a5b693e8c78a927b744c9618df95d40042b
ms.sourcegitcommit: 6b09412f7bf562f7c01ffa94ac44a3d0ea895e3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82086717"
---
# <a name="serial-controller-drivers-overview"></a>串行控制器驱动程序概述

所有版本的 Windows 都为串行控制器设备提供驱动程序支持。 术语 "*串行控制器*" 是指16550通用异步接收方（UART）或兼容的设备。 串行控制器具有串行端口，通过此端口，它与串行连接的外围设备进行通信。 为了支持串行通信，Windows 包含了 sys.databases 和 Serenum 驱动程序以及串行 framework 扩展的版本1和版本2（SerCx 和 SerCx2）。

## <a name="serialsys-and-serenumsys"></a>Sys.databases 和 Serenum

从 Windows 2000 开始，系统提供的串行驱动程序 Serial 支持独立串行端口、 [COM 端口](configuration-of-com-ports.md)和多端口板。 系统提供的串行枚举驱动程序 Serenum 枚举连接到串行端口的设备，该串行端口由 Serial 或兼容的串行端口驱动程序控制。 Serial 通常控制位于运行 Windows 的 PC 的情况下的 COM 端口（通常称为 COM1、COM2 等）。 这些端口与 RS-232 标准严格一致，但另外，还纳入了经过发展以支持 Pc 的事实标准（例如，电压级别、pin 连接和硬件流控制）。 有关详细信息，请参阅[使用 sys.databases 和 Serenum](using-serial-sys-and-serenum-sys.md)。

GitHub 上的 Windows 驱动程序示例存储库包含[序列](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial)和[Serenum](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serenum)驱动程序示例的源代码，它们的操作方式类似于，并且可以安装在收件箱和 Serenum 驱动程序的位置。

## <a name="sercx-and-sercx2"></a>SerCx 和 SerCx2

从 Windows 8 开始，SerCx 是系统提供的组件，它支持印刷电路板上集成电路间的串行通信。 SerCx 是内核模式驱动程序框架（KMDF）的扩展。 此扩展简化了串行控制器的自定义驱动程序的开发。 SerCx 通过处理串行控制器常见的很多处理任务来协助基于扩展的串行控制器驱动程序。 此驱动程序通过[SerCx 设备驱动程序接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)与 SerCx 通信。

从 Windows 8.1 开始，SerCx 由 SerCx2 取代。 SerCx2 对 SerCx 进行了很多改进，以降低串行控制器驱动程序的大小和复杂性。 特别是，SerCx2 免除了管理超时所需的处理工作的串行控制器驱动程序，并协调了需要访问串行控制器的 i/o 事务。 因此，串行控制器驱动程序更小且更简单。 串行控制器的硬件供应商提供基于扩展的串行控制器驱动程序，该驱动程序管理串行控制器中特定于硬件的功能，并依赖于 SerCx2 执行一般的串行控制器任务。 此驱动程序通过[SerCx2 设备驱动程序接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)与 SerCx2 通信。

有关 SerCx2 的详细信息，请参阅[使用系列 Framework 扩展的版本2（SerCx2）](using-version-2-of-the-serial-framework-extension.md)。

有关 driver framework 的常规信息，请参阅[使用 WDF 开发驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)

## <a name="in-this-section"></a>在本节中

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="serial-i-o-request-interface.md" data-raw-source="[Serial I/O Request Interface](serial-i-o-request-interface.md)">串行 I/O 请求接口</a></p></td>
<td><p>若要控制连接到串行控制器上某个端口的外围设备，客户端应用程序或外围设备驱动程序将 i/o 请求发送到端口。</p></td>
</tr>
<tr class="even">
<td><p><a href="differences-between-sercx2-and-serial-sys.md" data-raw-source="[Differences Between SerCx2.sys and Serial.sys](differences-between-sercx2-and-serial-sys.md)">SerCx2.sys 和 Serial.sys 之间的差异</a></p></td>
<td><p>尽管收件箱 Sercx2 驱动程序和 Serial 驱动程序组件都实现了<a href="serial-i-o-request-interface.md" data-raw-source="[serial I/O request interface](serial-i-o-request-interface.md)">串行 i/o 请求接口</a>，但这些组件不能互换。 它们旨在满足不同的需求集。</p></td>
</tr>
</tbody>
</table>
