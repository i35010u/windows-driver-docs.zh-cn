---
Description: 本节中的主题提供了一个 USB 管道，URBs i/o 请求，并描述了客户端驱动程序如何使用设备驱动程序接口（DDIs）将数据传入和传出 USB 设备。
title: 在 USB 客户端驱动程序中发送 USB 数据传输的概述
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: e9795e2af0697f98990f116c2079c30bdd6504be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844826"
---
# <a name="overview-of-sending-usb-data-transfers-in-usb-client-drivers"></a>在 USB 客户端驱动程序中发送 USB 数据传输的概述


本节中的主题提供有关 i/o 请求的 USB 管道和 URBs 的信息，并介绍客户端驱动程序如何使用设备驱动程序接口（DDIs）将数据传入和传出 USB 设备。




每次在主机控制器与 USB 设备之间移动数据时，将进行一次传输。 通常，可将 USB 传输广泛分类为控制传输和数据传输。 所有 USB 设备都必须支持控制传输，并可支持用于数据传输的终结点。 每种类型的传输与*USB 终结点*（设备中的缓冲区）的类型相关联。 控制传输与默认终结点相关联，并且数据传输使用单向终结点。 数据传输类型使用中断、大容量和同步终结点。 USB 驱动程序堆栈为设备支持的每个终结点创建一个称为*管道*的通信通道。 管道的一端是设备的终结点。 管道的另一端始终是主机控制器。

在将 i/o 请求发送到设备之前，客户端驱动程序必须从 USB 设备检索有关配置、接口、终结点、供应商和类特定描述符的信息。 此外，驱动程序还必须配置设备。 设备配置涉及到在每个接口中选择配置和备用设置等任务。 每个备用设置都可以指定一个或多个可用于数据传输的 USB 终结点。

有关设备配置的信息，请参阅[如何为 Usb 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)以及[如何在 usb 接口中选择备用设置](select-a-usb-alternate-setting.md)。

客户端驱动程序配置好设备后，该驱动程序可以访问当前所选替代设置中的每个终结点的 USB 驱动程序堆栈所创建的管道句柄。 若要将数据传输到终结点，客户端驱动程序会通过设置特定于请求类型的 URB 的格式来创建请求。

## <a name="in-this-section"></a>本部分内容


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
<td><p><a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">如何发送 USB 控件传输</a></p></td>
<td><p>本主题介绍了控件传输的结构，以及客户端驱动程序应如何向设备发送控制请求。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-get-usb-pipe-handles.md" data-raw-source="[How to enumerate USB pipes](how-to-get-usb-pipe-handles.md)">如何枚举 USB 管道</a></p></td>
<td><p>本主题概述了 USB 管道，并介绍了 USB 客户端驱动程序从 USB 驱动程序堆栈获取管道句柄所需的步骤。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">如何使用连续读取器读取 USB 管道中的数据</a></p></td>
<td><p>本主题介绍 WDF 提供的连续读取器对象。 本主题中的过程提供了有关如何配置对象并使用它从 USB 管道读取数据的分步说明。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to send USB bulk transfer requests](usb-bulk-and-interrupt-transfer.md)">如何发送 USB 批量传输请求</a></p></td>
<td><p>本主题提供有关 USB 批量传输的简要概述。 它还提供了有关客户端驱动程序如何从设备发送和接收大容量数据的分步说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to open and close static streams in a USB bulk endpoint](how-to-open-streams-in-a-usb-endpoint.md)">如何在 USB 批量终结点中打开和关闭静态流</a></p></td>
<td><p>本主题讨论静态流功能，并说明 USB 客户端驱动程序如何在 USB 3.0 设备的大容量终结点中打开和关闭流。</p></td>
</tr>
<tr class="even">
<td><p><a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">如何将数据传输到 USB 同步终结点</a></p></td>
<td><p>本主题介绍客户端驱动程序如何构建 USB 请求块（URB），以便在 USB 设备中将数据传入和传出同步终结点。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">如何发送链式 MDLs</a></p></td>
<td><p>在本主题中，你将了解有关 USB 驱动程序堆栈中链式 MDLs 功能的信息，以及客户端驱动程序如何以<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl" data-raw-source="[&lt;strong&gt;MDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)"><strong>MDL</strong></a>结构链形式发送传输缓冲区。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-recover-from-usb-pipe-errors.md" data-raw-source="[How to recover from USB pipe errors](how-to-recover-from-usb-pipe-errors.md)">如何从 USB 管道错误中恢复</a></p></td>
<td><p>本主题提供有关在将数据传输到 USB 管道失败时可尝试执行的步骤的信息。 本主题中所述的机制介绍了对批量、中断和同步管道的中止、重置和循环端口操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-bandwidth-allocation.md" data-raw-source="[USB Bandwidth Allocation](usb-bandwidth-allocation.md)">USB 带宽分配</a></p></td>
<td><p>本部分提供有关仔细管理 USB 带宽的指南。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



