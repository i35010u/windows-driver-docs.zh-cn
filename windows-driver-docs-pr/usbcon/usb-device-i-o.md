---
Description: 在本部分中的主题提供 USB 管道 URBs 的 I/O 请求，并介绍客户端驱动程序如何使用设备驱动程序接口 (DDIs) 将数据传入和传出的 USB 设备。
title: 在 USB 客户端驱动程序中发送 USB 数据传输
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: dd92cf4ac5eb08d2123c28fa604672ab74df39aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331609"
---
# <a name="sending-usb-data-transfers-in-usb-client-drivers"></a>在 USB 客户端驱动程序中发送 USB 数据传输


在本部分中的主题提供有关 USB 管道和 URBs I/O 请求的信息，并介绍客户端驱动程序如何使用设备驱动程序接口 (DDIs) 来传输数据传入和传出的 USB 设备。




每次主控制器和 USB 设备之间移动数据时，传输将会发生。 可以在控件中广泛地分为 USB 传输的一般情况下，传输和数据传输。 所有 USB 设备必须支持的控制转移，并且可以对数据传输支持终结点。 每种类型的传输是与类型的关联*USB 终结点*（设备中的缓冲区）。 控制传输与默认终结点相关联，并且数据传输使用单向终结点。 数据传输类型使用中断、 批量和同步终结点。 USB 驱动程序堆栈创建名为一个信道*管道*设备支持的每个终结点。 在管道的一端是设备的终结点。 管道另一端始终是主控制器。

向设备发送的 I/O 请求之前, 的客户端驱动程序必须从 USB 设备检索有关配置、 接口、 终结点、 供应商，以及特定于类的描述符信息。 此外，驱动程序还必须配置设备。 设备配置涉及到任务，例如选择配置和替代设置中的每个接口。 每个备用设置可以指定一个或多个 USB 终结点可用于数据传输。

有关设备配置的信息，请参阅[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)并[如何在 USB 界面中选择一项备用设置](select-a-usb-alternate-setting.md)。

客户端驱动程序已配置设备后，该驱动程序有权访问由在当前所选的备用设置每个终结点的 USB 驱动程序堆栈创建的管道句柄。 若要将数据传输到一个终结点，客户端驱动程序的格式设置特定于类型的请求 URB 创建请求。

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
<td><p><a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">如何发送 USB 控制传输</a></p></td>
<td><p>本主题介绍控制传输和如何客户端驱动程序应将控制请求发送到设备的结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-get-usb-pipe-handles.md" data-raw-source="[How to enumerate USB pipes](how-to-get-usb-pipe-handles.md)">如何枚举 USB 管道</a></p></td>
<td><p>本主题概述了 USB 管道，并介绍了通过 USB 客户端驱动程序从 USB 驱动程序堆栈获取管道句柄所必需的步骤。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">如何使用来从 USB 管道读取数据的连续读取器</a></p></td>
<td><p>本主题介绍 WDF 提供持续的读取器对象。 本主题中的过程提供有关如何配置对象并使用它从 USB 管道读取数据的分步说明。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to send USB bulk transfer requests](usb-bulk-and-interrupt-transfer.md)">如何发送 USB 大容量传输请求</a></p></td>
<td><p>本主题提供有关 USB 批量传输的简要概述。 它还提供有关如何对客户端驱动程序可以发送和接收来自设备的大容量数据的分步说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to open and close static streams in a USB bulk endpoint](how-to-open-streams-in-a-usb-endpoint.md)">如何打开和关闭 USB 大容量终结点中的静态流</a></p></td>
<td><p>本主题讨论了静态流功能并说明如何打开和关闭的流，大容量的 USB 3.0 设备终结点中 USB 客户端驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">如何将数据传输到 USB 等时终结点</a></p></td>
<td><p>本主题介绍客户端驱动程序可以如何生成 USB 请求块 (URB) 将在同步终结点在 USB 设备中的数据传输。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">如何发送链接 MDLs</a></p></td>
<td><p>在本主题中，您将学习有关 USB 驱动程序堆栈，并且如何客户端驱动程序可以发送的传输缓冲区作为链中的链接 MDLs 功能<a href="https://msdn.microsoft.com/library/windows/hardware/ff554414" data-raw-source="[&lt;strong&gt;MDL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554414)"> <strong>MDL</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-recover-from-usb-pipe-errors.md" data-raw-source="[How to recover from USB pipe errors](how-to-recover-from-usb-pipe-errors.md)">如何从 USB 管道错误中恢复</a></p></td>
<td><p>本主题提供有关步骤的信息可以尝试在数据传输到 USB 管道时失败。 本主题涵盖中所述的机制中止，重置，并循环大容量、 中断，并等时管道上的端口操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-bandwidth-allocation.md" data-raw-source="[USB Bandwidth Allocation](usb-bandwidth-allocation.md)">USB 带宽分配</a></p></td>
<td><p>本部分提供有关 USB 带宽慎重地管理的指南。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



