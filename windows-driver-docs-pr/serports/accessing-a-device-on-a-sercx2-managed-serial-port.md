---
title: 访问 SerCx2 托管串行端口上的设备
description: SerCx2 和串行控制器驱动程序共同管理将设备永久连接到的串行端口。
ms.assetid: EF7F42D3-21A5-42F8-86AB-897281DF4F18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9be07bb7507f4e2cbda7c0d1ef012fc16d010e6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184215"
---
# <a name="accessing-a-device-on-a-sercx2-managed-serial-port"></a>访问 SerCx2 托管串行端口上的设备


SerCx2 和串行控制器驱动程序共同管理将设备永久连接到的串行端口。 若要访问 SerCx2 管理的串行端口上的外围设备，外围设备驱动程序会打开与串行端口的逻辑连接，并获得表示此连接的文件句柄。 然后，驱动程序使用此句柄将 i/o 请求发送到端口。

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
<td><p><a href="peripheral-drivers-for-devices-on-sercx2-managed-serial-ports.md" data-raw-source="[Peripheral Drivers for Devices on SerCx2-Managed Serial Ports](peripheral-drivers-for-devices-on-sercx2-managed-serial-ports.md)">SerCx2 托管串行端口上的设备的外设驱动程序</a></p></td>
<td><p>通常，由 SerCx2 管理的串行端口会永久连接到外围设备。 此设备由向串行端口发送 i/o 请求的外围设备驱动程序控制。 这些请求将数据传入和传出设备，并配置串行端口的状态。 外设驱动程序发送的 i/o 请求由 SerCx2 和关联的串行控制器驱动程序共同处理。</p></td>
</tr>
<tr class="even">
<td><p><a href="opening-a-sercx2-managed-serial-port.md" data-raw-source="[Opening a SerCx2-Managed Serial Port](opening-a-sercx2-managed-serial-port.md)">打开 SerCx2 托管串行端口</a></p></td>
<td><p>如果外设驱动程序控制串行端口上由 SerCx2 和串行控制器驱动程序共同管理的设备，则驱动程序可以打开到此端口的逻辑连接，然后通过端口将 i/o 请求发送到设备。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-handling-of-read-and-write-requests.md" data-raw-source="[SerCx2 Handling of Read and Write Requests](sercx2-handling-of-read-and-write-requests.md)">SerCx2 对读取和写入请求的处理</a></p></td>
<td><p>外设驱动程序将写入 (发送 <a href="https://docs.microsoft.com/previous-versions/ff546904(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](/previous-versions/ff546904(v=vs.85))"><strong>IRP_MJ_WRITE</strong></a>) ，并 (<a href="https://docs.microsoft.com/previous-versions/ff546883(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](/previous-versions/ff546883(v=vs.85))"><strong>IRP_MJ_READ</strong></a>) 请求发送到串行控制器上的端口，以将数据传输到连接到该端口的外围设备并将其传输到该端口。 SerCx2 处理这些请求的方式经过良好定义，即使请求超时或被取消。</p></td>
</tr>
<tr class="even">
<td><p><a href="reading-data-from-a-sercx2-managed-serial-port.md" data-raw-source="[Reading Data from a SerCx2-Managed Serial Port](reading-data-from-a-sercx2-managed-serial-port.md)">从 SerCx2 托管串行端口读取数据</a></p></td>
<td><p>串行控制器 (或 UART) 通常包含接收 FIFO。 此 FIFO 提供从连接到串行端口的外围设备接收的数据的硬件控制缓冲。 若要从接收 FIFO 中读取数据，此设备的外围设备驱动程序会向串行端口发送 <a href="https://docs.microsoft.com/previous-versions/ff546883(v=vs.85)" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](/previous-versions/ff546883(v=vs.85))"><strong>IRP_MJ_READ</strong></a>) 请求的读取 (。</p></td>
</tr>
</tbody>
</table>

 

 

