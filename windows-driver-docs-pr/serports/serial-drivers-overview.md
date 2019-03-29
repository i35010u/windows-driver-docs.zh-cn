---
title: 串行控制器驱动程序概述
description: 所有版本的 Windows 都提供的串行控制器设备驱动程序支持。
ms.assetid: 1EA0221E-0F68-429B-9DA5-4AE2D3394A09
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df26e9220e3976f482deb9035faf3380b1f45b05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568187"
---
# <a name="serial-controller-drivers-overview"></a>串行控制器驱动程序概述


所有版本的 Windows 都提供的串行控制器设备驱动程序支持。 术语*串行控制器*指 16550 通用异步收发-器 (UART) 或兼容的设备。 串行控制器具有与串行连接的外围设备通过其通信的串行端口。 若要支持串行通信，Windows 包括 Serial.sys 和 Serenum.sys 驱动程序和版本 1 和 2 个串行 framework 扩展 （SerCx 和 SerCx2）。

## <a name="serialsys-and-serenumsys"></a>Serial.sys 和 Serenum.sys


从 Windows 2000 开始，该系统提供串行驱动程序，Serial.sys，支持独立的串行端口[COM 端口](configuration-of-com-ports.md)，和多端口的板。 系统提供的串行枚举驱动程序，Serenum.sys，枚举到由 Serial.sys 或兼容的串行端口驱动程序控制的串行端口连接的设备。 通常为 Serial.sys 控件位于正在运行 Windows 的 PC 的大小写的 COM 端口 （通常名为 COM1、 COM2 等等）。 这些端口松散符合 RS-232 标准，但此外合并已演变成将支持 Pc 的业界标准 （例如，对于电压水平、 pin 连接和硬件流控制）。 有关详细信息，请参阅[使用 Serial.sys 和 Serenum.sys](using-serial-sys-and-serenum-sys.md)。

GitHub 上的 Windows 驱动程序示例存储库包含的源代码[串行](https://go.microsoft.com/fwlink/p/?LinkId=617962)并[Serenum](https://go.microsoft.com/fwlink/p/?LinkId=617961)驱动程序示例，它类似于运行且可以安装取代收件箱 Serial.sys和 Serenum.sys 驱动程序。

## <a name="sercx-and-sercx2"></a>SerCx 和 SerCx2


从 Windows 8 开始，SerCx 是支持串行通信之间集成线路上印刷电路板的系统提供的组件。 SerCx 是扩展[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF)。 此扩展简化了为串行控制器的自定义驱动程序的开发。 SerCx 协助扩展基于串行控制器驱动程序处理多项所共有的串行控制器的处理任务。 此驱动程序与通过 SerCx [SerCx 设备驱动程序接口](https://msdn.microsoft.com/library/windows/hardware/dn265348)。

从 Windows 8.1 开始，将被 SerCx2 取代 SerCx。 SerCx2 SerCx 减少的大小和复杂性的串行控制器驱动程序都有很多改进。 具体而言，SerCx2 使所需管理超时值，以及协调访问串行控制器会争夺 I/O 事务的处理工作的串行控制器驱动程序。 因此，串行控制器驱动程序是更小且更简单。 串行控制器的硬件供应商提供的扩展插件基于串行控制器驱动程序管理的特定于硬件的函数中的串行控制器，并且依赖于 SerCx2 执行常规序列控制器任务。 此驱动程序与通过 SerCx2 [SerCx2 设备驱动程序接口](https://msdn.microsoft.com/library/windows/hardware/dn265349)。

有关 SerCx2 详细信息，请参阅[串行框架扩展 (SerCx2) 的使用版本 2](using-version-2-of-the-serial-framework-extension.md)。

## <a name="in-this-section"></a>本节内容


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
<td><p><a href="serial-i-o-request-interface.md" data-raw-source="[Serial I/O Request Interface](serial-i-o-request-interface.md)">串行 I/O 请求接口</a></p></td>
<td><p>若要控制外围设备连接到串行控制器，客户端上的端口的应用程序或外围设备驱动程序将发送到端口的输入/输出请求。</p></td>
</tr>
<tr class="even">
<td><p><a href="differences-between-sercx2-and-serial-sys.md" data-raw-source="[Differences Between SerCx2.sys and Serial.sys](differences-between-sercx2-and-serial-sys.md)">SerCx2.sys 和 Serial.sys 之间的差异</a></p></td>
<td><p>尽管的收件箱 Sercx2.sys 和 Serial.sys 驱动程序组件这两个实现<a href="serial-i-o-request-interface.md" data-raw-source="[serial I/O request interface](serial-i-o-request-interface.md)">串行 I/O 请求接口</a>，这些组件不能互换。 它们旨在满足不同的要求。</p></td>
</tr>
</tbody>
</table>

 

 

 




