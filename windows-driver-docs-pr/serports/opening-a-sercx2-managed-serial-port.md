---
title: 打开 SerCx2 托管串行端口
description: 如果您外围设备的驱动程序控制 SerCx2 和串行控制器驱动程序由联合管理的串行端口上的设备，您的驱动程序可以打开与此端口的逻辑连接，然后通过该端口向设备发送的 I/O 请求。
ms.assetid: CBFE1789-0D60-480A-B467-4690DFF88AAC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a68d07a9106363dd2f126630059d6b875076770c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331133"
---
# <a name="opening-a-sercx2-managed-serial-port"></a>打开 SerCx2 托管串行端口


从 Windows 8.1，串行 framework 扩展的版本 2 (SerCx2) 一同使用来管理上的串行控制器的串行端口的串行控制器驱动程序。 如果您外围设备的驱动程序控制 SerCx2 和串行控制器驱动程序由联合管理的串行端口上的设备，您的驱动程序可以打开与此端口的逻辑连接，然后通过该端口向设备发送的 I/O 请求。

串行控制器是 16550 通用异步接收器/转换器 (UART) 或兼容的设备。 有关详细信息，请参阅[串行控制器驱动程序概述](serial-drivers-overview.md)。

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
<td><p><a href="connection-ids-for-serially-connected-peripheral-devices.md" data-raw-source="[Connection IDs for Serially Connected Peripheral Devices](connection-ids-for-serially-connected-peripheral-devices.md)">连接 Id 的串行连接的外围设备</a></p></td>
<td><p>如果编写用于连接到串行端口由 SerCx2 管理的外围设备的驱动程序，包括驱动程序收到的硬件资源的列表<em>连接 ID</em>封装设备连接信息从平台固件中。</p></td>
</tr>
<tr class="even">
<td><p><a href="connecting-a-umdf-peripheral-device-driver-to-a-serial-port.md" data-raw-source="[Connecting a UMDF Peripheral Driver to a Serial Port](connecting-a-umdf-peripheral-device-driver-to-a-serial-port.md)">连接到串行端口的外设的 UMDF 驱动程序</a></p></td>
<td><p>外围设备 SerCx2 托管的串行端口上的 UMDF 驱动程序需要特定硬件资源操作设备。 这些资源中包含的是该驱动程序必须打开的逻辑连接到串行端口的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="connecting-a-kmdf-peripheral-device-driver-to-a-serial-port.md" data-raw-source="[Connecting a KMDF Peripheral Driver to a Serial Port](connecting-a-kmdf-peripheral-device-driver-to-a-serial-port.md)">连接到串行端口 KMDF 外围设备驱动程序</a></p></td>
<td><p>外围设备 SerCx2 托管的串行端口上的 KMDF 驱动程序需要特定硬件资源操作设备。 这些资源中包含的是该驱动程序必须打开的逻辑连接到串行端口的信息。</p></td>
</tr>
</tbody>
</table>

 

 

 




