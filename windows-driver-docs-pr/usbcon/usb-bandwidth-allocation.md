---
description: 本部分提供有关仔细管理 USB 带宽的指南。
title: USB 带宽分配
ms.date: 04/20/2017
ms.assetid: a1533825-a28f-45eb-9a54-c7298022c385
ms.localizationpriority: medium
ms.openlocfilehash: a5df15b24d10ec2dc3e23be286c8dd05c5899456
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968750"
---
# <a name="usb-bandwidth-allocation"></a>USB 带宽分配


本部分提供有关仔细管理 USB 带宽的指南。

每个 USB 客户端驱动程序负责将其使用的 USB 带宽降到最低，并尽快将未使用的带宽返回到可用带宽池。

本节包括下列主题：

## <a name="why-is-my-usb-driver-getting-out-of-bandwidth-errors"></a>为什么 USB 驱动程序出现带宽错误？


USB 总线上的带宽争用来自多个源（硬件和软件），因此很难准确预测可用于 USB 客户端驱动程序的带宽量。 USB 主机控制器需要为其操作指定一定量的带宽，但所需的量取决于控制器的速度是否很高，因此它将因系统而异。 高速运行的 USB 集线器有时必须在高速度上游端口和低速设备之间转换事务，而此转换过程会消耗带宽。 但事务转换是否需要带宽取决于所连接的设备类型和设备树的拓扑。

带宽资源最严重的压力通常来自独占带宽的 USB 客户端驱动程序。 系统按首先服务的原则分配带宽。 如果加载的第一个 USB 驱动程序请求所有可用带宽，则稍后加载的 USB 驱动程序将不会获得其设备的所有带宽。 出现这种情况时，系统无法配置设备，并且无法枚举设备。 由于枚举失败的原因通常不明显，因此可能导致用户体验不佳。

有时，客户端驱动程序将使用高速中断传输来排出可用带宽。 但最常见的情况是，客户端驱动程序为按同步传输分配过多的带宽，然后无法及时释放带宽。 系统会保留分配的带宽，直到请求它的驱动程序关闭其终结点 (通过打开另一个终结点) ，或删除为其分配带宽的设备。 系统不为大容量传输分配有保证的带宽，因此大容量传输永远不会导致枚举失败。 但是，批量传输设备的性能取决于为定期 (同步和中断) 传输的设备分配的带宽量。

USB 2.0 规范要求同步设备在其默认接口设置上具有零带宽终结点。 这可以确保在函数驱动程序打开非默认接口之前不会为设备保留带宽，而是有助于防止在设备配置过程中过多的带宽请求导致的枚举失败。 但是，它不会阻止客户端驱动程序在配置其设备后分配过多的带宽，从而阻止其他设备正常运行。

正确的带宽管理的关键是：系统中执行同步传输的每个 USB 设备都必须为包含同步终结点的每个接口提供多个备用 (Alt) 设置，并且客户端驱动程序必须明智地使用这些 Alt 设置。 客户端驱动程序应该首先请求最大带宽的接口设置。 如果请求失败，客户端驱动程序应请求具有更小、更小带宽的接口设置，直到请求成功。

例如，假设网络摄像机设备具有以下接口：

接口 0 (默认接口设置：默认设置中没有非零同步带宽的终结点) 

同步终结点1：最大数据包大小 = 0 字节

同步终结点2：最大数据包大小 = 0 字节

接口 0 Alt 设置1

同步终结点1：最大数据包大小 = 256 字节

同步终结点2：最大数据包大小 = 256 字节

接口 0 Alt 设置2

同步终结点1：最大数据包大小 = 512 字节

同步终结点2：最大数据包大小 = 512 字节

网络摄像机的驱动程序将网络摄像机配置为在初始化时使用默认接口设置。 默认设置没有同步带宽，因此在初始化期间使用默认设置可避免网络摄像机可能无法枚举的危险，因为对同步带宽的请求失败。

当客户端驱动程序准备进行同步传输时，它应尝试使用 Alt 设置2，因为 Alt 设置2的数据包大小最大。 如果请求失败，则驱动程序可以再次尝试使用 Alt 设置1。 由于 Alt 设置1需要较少的带宽，此请求可能会成功，即使第一个请求失败也是如此。 多个 Alt 设置允许驱动程序在放弃之前进行多次尝试。

在网络摄像机空闲后，通过再次选择默认设置，可以将分配的带宽返回到可用带宽池。

从 Windows Vista 开始，用户可以通过在设备管理器中检查控制器的属性，来查看 USB 控制器分配了多少带宽。 选择控制器的属性，然后在 "高级" 选项卡下查看。此读数并不表示 USB 集线器分配给事务转换的带宽量。

报告 USB 控制器的带宽使用情况的设备管理器功能在 Windows XP 中无法正常运行。

 
## <a name="usb-transfer-and-packet-sizes"></a>USB 传输和数据包大小


本主题介绍各种版本的 Windows 操作系统中允许的 USB 传输大小。

-   [最大传输大小](#maximum-transfer-size)
-   [最大数据包大小](#maximum-packet-size)
-   [读取传输缓冲区的最大数据包大小限制](#maximum-packet-size-restriction-on-read-transfer-buffers)
-   [用短数据包分隔写入传输](#delimiting-write-transfers-with-short-packets)

### <a name="maximum-transfer-size"></a>最大传输大小


*最大传输大小*指定 USB 驱动程序堆栈中的硬编码限制。 由于系统资源限制，传输大小低于这些限制可能会失败。 若要避免这种类型的故障并确保 Windows 的所有版本之间的兼容性，请避免使用较大的传输大小进行 USB 传输。

> **注意**  
>
> 在 Windows XP、Windows Server 2003 和更高版本中， [**USBD \_ 管道 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)结构的**MaximumTransferSize**成员已过时。 USB 驱动程序堆栈忽略组合和非复合设备的 **MaximumTransferSize** 中的值。
>
> 在 Windows 2000 中，USB 驱动程序堆栈会将 **MaximumTransferSize** 初始化为 USBD \_ 默认的 \_ 最大 \_ 传输 \_ 大小。 客户端驱动程序可以在配置设备时设置较小的值。 对于复合设备，每个函数的客户端驱动程序只能为非默认接口设置中的管道更改 **MaximumTransferSize** 。

USB 传输大小服从以下限制：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>传输管道</th>
<th>Windows 8.1，Windows 8</th>
<th>Windows 7、Windows Vista</th>
<th>Windows XP 和 Windows Server 2003</th>
<th>Windows 2000</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>控件</td>
<td><p>64K，适用于 SuperSpeed 和高速 (xHCI) </p>
<p>4K 适用于全速 (xHCI，EHCI，UHCI，OHCI) </p>
<p>对于 UHCI，为默认终结点上的 4K;非默认控制管道上的64K</p></td>
<td><p>64K (EHCI) </p>
<p>4K (EHCI、UHCI、OHCI) 的全速和低速</p>
<p>对于 UHCI，为默认终结点上的 4K;非默认控制管道上的 64K (UHCI) </p></td>
<td><p>64K (EHCI) </p>
<p>4K (EHCI、UHCI、OHCI) 的全速和低速</p>
<p>对于 UHCI，为默认终结点上的 4K;非默认控制管道上的 64K (UHCI) </p></td>
<td><p>默认终结点上的 4K;非默认控制管道上的 64K (OHCI) </p></td>
</tr>
<tr class="even">
<td>中断</td>
<td><p>4MB，SuperSpeed (，xHCI，EHCI，UHCI，OHCI) </p></td>
<td><p>4MB，适用于 (EHCI、UHCI、OHCI) 的高、全速和低速度</p></td>
<td>无限制</td>
<td><p>不确定的 (OHCI) </p></td>
</tr>
<tr class="odd">
<td>批量</td>
<td><p>适用于 SuperSpeed 的 32MB (xHCI) </p>
<p>4MB，适用于高和全速 (xHCI) </p>
<p>4MB，适用于高和全速 (EHCI 和 UHCI) </p>
<p>256K 全速 (OHCI) </p></td>
<td><p>4 MB，适用于高和全速 (EHCI，UHCI) </p>
<p>用于全速 (OHCI 的 256K) </p></td>
<td><p>对于高和全速 (EHCI) </p>
<p>不确定的 (UHCI) </p>
<p>用于全速 (OHCI 的 256K) </p></td>
<td><p>不确定的 (OHCI) </p></td>
</tr>
<tr class="even">
<td>量</td>
<td><p>1024 <em> <strong>wBytesPerInterval</strong> (参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor" data-raw-source="[&lt;strong&gt;USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor)"><strong>USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR</strong></a>) SUPERSPEED (xHCI) </p>
<p>1024 </em> <strong>MaximumPacketSize</strong> (for xHCI，EHCI) </p>
<p>256 * <strong>MaximumPacketSize</strong> for 全速 (XHCI，EHCI) </p>
<p>64K 的全速 (UHCI，OHCI) </p></td>
<td><p>1024 * <strong>MaximumPacketSize</strong> ，用于高速 (EHCI) </p>
<p>256 * <strong>MaximumPacketSize</strong> 以获取全速 (EHCI) </p>
<p>64K 的全速 (UHCI，OHCI) </p></td>
<td><p>1024 * <strong>MaximumPacketSize</strong> ，适用于高速 (EHCI) </p>
<p>256 * <strong>MaximumPacketSize</strong> 以获取全速 (EHCI) </p>
<p>64K 的全速 (UHCI，OHCI) </p></td>
<td><p>64K 的全速 (OHCI) </p></td>
</tr>
</tbody>
</table>

 

使用 **MaximumTransferSize** 限制传输大小不会直接影响设备消耗的带宽量。 客户端驱动程序必须更改接口设置，或限制在[**USBD \_ 管道 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)的**MaximumPacketSize**成员中设置的最大数据包大小。

### <a name="maximum-packet-size"></a>最大数据包大小


*最大数据包大小*由端点描述符的**wMaxPacketSize**字段定义。 客户端驱动程序可以在设备的选择-接口请求中控制 USB 数据包大小。 更改此值不会更改设备上的 **wMaxPacketSize** 。

对于该请求， [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb) 中的是管道的 [**USBD \_ 管道 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information) 结构。 在该结构中，

-   修改[**USBD \_ 管道 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)结构的**MaximumPacketSize**成员。 将其设置为小于或等于 "当前接口" 设置的 "设备固件" 中定义的 **wMaxPacketSize** 的值。
-   \_ \_ \_ \_ 在**PipeFlags**成员[**USBD \_ 管道 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)结构中设置 USBD PF 更改最大数据包标志。

有关选择接口设置的信息，请参阅 [如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)。

### <a name="maximum-packet-size-restriction-on-read-transfer-buffers"></a>读取传输缓冲区的最大数据包大小限制


当客户端驱动程序发出读取请求时，传输缓冲区必须是最大数据包大小的倍数。 即使驱动程序需要的数据小于最大数据包大小，它仍必须请求整个数据包。 如果设备发送的数据包小于 (短数据包) 的最大大小，则表明传输已完成。

**注意**  

在较旧的控制器上，客户端驱动程序可以重写此行为。 在 data transfer [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)的**TransferFlags**成员中，客户端驱动程序必须设置 USBD \_ SHORT \_ transfer \_ OK 标志。 该标志允许设备发送小于 **wMaxPacketSize**的数据包。

在 xHCI 主机控制器上， \_ \_ \_ 为大容量和中断终结点忽略 USBD SHORT 传输正常。 在 EHCI 控制器上传输短数据包不会导致错误。

在 EHCI 主机控制器上， \_ \_ \_ 大容量和中断终结点的 USBD 短传输正常。

在 UHCI 和 OHCI 主机控制器上，如果 \_ \_ \_ 没有为大容量传输或中断传输设置 USBD short transfer transfer，则短数据包传输会暂停终结点，并返回一个错误代码用于传输。

### <a name="delimiting-write-transfers-with-short-packets"></a>用短数据包分隔写入传输


当写入设备时，USB 驱动程序堆栈驱动程序不会对数据包大小施加相同的限制。 某些客户端驱动程序必须频繁传输少量的控制数据来管理其设备。 在这种情况下，将数据传输限制为大小相同的数据包是不切实际的。 因此，在数据写入过程中，驱动程序堆栈不会将任何特殊意义分配给大小小于终结点的最大大小的数据包。 这允许客户端驱动程序将大容量传输到大于或等于最大值的多个 URBs。

驱动程序必须通过不超过最大大小的数据包来结束传输，或者用长度为零的数据包分隔传输结束。 直到驱动程序发送一个小于 *wMaxPacketSize*的数据包，才能完成传输。 如果传输大小是最大值的倍数，则驱动程序必须发送一个长度为零的分隔数据包，以显式终止传输

根据 USB 规范的要求，用长度为零的数据包来界定数据传输是客户端驱动程序的责任。 USB 驱动程序堆栈不会自动生成这些数据包。

 
## <a name="delimiting-usb-data-transfers-with-packets-smaller-than-wmaxpacketsize"></a>用小于 wMaxPacketSize 的数据包分隔 USB 数据传输


兼容的 USB 2.0/1.1 驱动程序必须将最大大小的数据包传输 (*wMaxPacketSize*) ，然后通过不超过最大大小的数据包结束传输，或者通过长度为零的数据包来界定传输的结束时间。 直到驱动程序发送一个小于 *wMaxPacketSize*的数据包，才能完成传输。 如果传输大小是最大值的倍数，则驱动程序必须发送一个长度为零的分隔数据包，以显式终止传输

根据 USB 规范的要求，用长度为零的数据包来界定数据传输是设备驱动程序的责任。 系统 USB 堆栈不会自动生成这些数据包。


 




