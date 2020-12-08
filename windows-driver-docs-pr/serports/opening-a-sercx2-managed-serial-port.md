---
title: 打开 SerCx2 托管串行端口
description: 如果外设驱动程序控制串行端口上由 SerCx2 和串行控制器驱动程序共同管理的设备，则驱动程序可以打开到此端口的逻辑连接，然后通过端口将 i/o 请求发送到设备。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86651fce5f8ed7a9876c4a343fc387a44e749007
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805013"
---
# <a name="opening-a-sercx2-managed-serial-port"></a>打开 SerCx2 托管串行端口


从 Windows 8.1 开始，版本2的串行框架扩展 (SerCx2) 与串行控制器驱动程序一起工作，用于管理串行控制器上的串行端口。 如果外设驱动程序控制串行端口上由 SerCx2 和串行控制器驱动程序共同管理的设备，则驱动程序可以打开到此端口的逻辑连接，然后通过端口将 i/o 请求发送到设备。

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
<td><p><a href="connection-ids-for-serially-connected-peripheral-devices.md" data-raw-source="[Connection IDs for Serially Connected Peripheral Devices](connection-ids-for-serially-connected-peripheral-devices.md)">串行连接的外围设备的连接 ID</a></p></td>
<td><p>如果为连接到由 SerCx2 管理的串行端口的外围设备编写驱动程序，则该驱动程序接收的硬件资源列表包括一个 <em>连接 ID</em> ，该 ID 封装了平台固件中的设备连接信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="connecting-a-umdf-peripheral-device-driver-to-a-serial-port.md" data-raw-source="[Connecting a UMDF Peripheral Driver to a Serial Port](connecting-a-umdf-peripheral-device-driver-to-a-serial-port.md)">将 UMDF 外设驱动程序连接到串行端口</a></p></td>
<td><p>适用于 SerCx2 管理的串行端口上的外围设备的 UMDF 驱动程序需要某些硬件资源才能运行设备。 这些资源包含驱动程序打开串行端口逻辑连接所需的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="connecting-a-kmdf-peripheral-device-driver-to-a-serial-port.md" data-raw-source="[Connecting a KMDF Peripheral Driver to a Serial Port](connecting-a-kmdf-peripheral-device-driver-to-a-serial-port.md)">将 KMDF 外设驱动程序连接到串行端口</a></p></td>
<td><p>SerCx2 管理的串行端口上的外围设备的 KMDF 驱动程序需要某些硬件资源来运行设备。 这些资源包含驱动程序打开串行端口逻辑连接所需的信息。</p></td>
</tr>
</tbody>
</table>

 

 

 




