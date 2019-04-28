---
title: 访问 SerCx2 托管串行端口上的设备
description: SerCx2 和串行控制器驱动程序合作共同管理永久连接到外围设备的串行端口。
ms.assetid: EF7F42D3-21A5-42F8-86AB-897281DF4F18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea57350c220ff0ed11be014f3d8b32beffaaf5a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345297"
---
# <a name="accessing-a-device-on-a-sercx2-managed-serial-port"></a>访问 SerCx2 托管串行端口上的设备


SerCx2 和串行控制器驱动程序合作共同管理永久连接到外围设备的串行端口。 若要访问 SerCx2 托管的串行端口上的外围设备，您外围设备的驱动程序打开串行端口的逻辑连接，并获取文件句柄来表示此连接。 然后驱动程序使用此句柄将 I/O 请求发送到端口。

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
<td><p><a href="peripheral-drivers-for-devices-on-sercx2-managed-serial-ports.md" data-raw-source="[Peripheral Drivers for Devices on SerCx2-Managed Serial Ports](peripheral-drivers-for-devices-on-sercx2-managed-serial-ports.md)">外围 SerCx2 托管串行端口上的设备驱动程序</a></p></td>
<td><p>通常情况下，由 SerCx2 串行端口已永久连接到外围设备。 此设备受将 I/O 请求发送到串行端口的外围设备驱动程序。 这些请求传输设备数据和配置的串行端口的状态。 由 SerCx2 和关联的串行控制器驱动程序，共同处理发送的外围设备驱动程序的 I/O 请求。</p></td>
</tr>
<tr class="even">
<td><p><a href="opening-a-sercx2-managed-serial-port.md" data-raw-source="[Opening a SerCx2-Managed Serial Port](opening-a-sercx2-managed-serial-port.md)">打开 SerCx2 托管串行端口</a></p></td>
<td><p>如果您外围设备的驱动程序控制 SerCx2 和串行控制器驱动程序由联合管理的串行端口上的设备，您的驱动程序可以打开与此端口的逻辑连接，然后通过该端口向设备发送的 I/O 请求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sercx2-handling-of-read-and-write-requests.md" data-raw-source="[SerCx2 Handling of Read and Write Requests](sercx2-handling-of-read-and-write-requests.md)">SerCx2 处理读取和写入请求</a></p></td>
<td><p>外围设备的驱动程序将发送写入 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff546904" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546904)"><strong>IRP_MJ_WRITE</strong></a>) 和读取 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff546883" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546883)"><strong>IRP_MJ_READ</strong></a>) 到串行控制器上的端口的请求传输数据传入和传出外围设备连接到的端口。 在其中 SerCx2 处理这些请求的方式是有明确定义，即使请求超时或被取消。</p></td>
</tr>
<tr class="even">
<td><p><a href="reading-data-from-a-sercx2-managed-serial-port.md" data-raw-source="[Reading Data from a SerCx2-Managed Serial Port](reading-data-from-a-sercx2-managed-serial-port.md)">从 SerCx2 托管串行端口读取数据</a></p></td>
<td><p>串行控制器 （或 UART） 通常包括接收先进先出。 此 FIFO 提供了硬件控制从外围设备连接到串行端口接收的数据缓冲。 若要从接收 FIFO 读取数据，此设备的外围设备驱动程序发送读取 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff546883" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546883)"><strong>IRP_MJ_READ</strong></a>) 到串行端口的请求。</p></td>
</tr>
</tbody>
</table>

 

 

 




