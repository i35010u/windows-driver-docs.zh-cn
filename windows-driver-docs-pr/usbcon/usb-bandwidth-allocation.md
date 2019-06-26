---
Description: 本部分提供有关 USB 带宽慎重地管理的指南。
title: USB 带宽分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e431ce8e26de70c6f7f338c9a7ad93d0c7cf5ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369531"
---
# <a name="usb-bandwidth-allocation"></a>USB 带宽分配


本部分提供有关 USB 带宽慎重地管理的指南。

它负责的每个 USB 客户端驱动程序，以最小化它使用 USB 带宽并尽可能立即返回到可用带宽池未使用的带宽。

本部分包括以下主题：

## <a name="why-is-my-usb-driver-getting-out-of-bandwidth-errors"></a>为什么我的 USB 驱动程序即将超出带宽错误？


USB 总线上的带宽的争用情况来自多个源、 硬件和软件，因此很难预测准确带宽量将可供 USB 客户端驱动程序。 USB 主控制器操作所需带宽一定量的但依赖于控制器是高速度，因此它将在变化系统之间所需的量。 运行高速的 USB 集线器有时必须转换高速上游端口和下游，低速度设备之间的事务并在此转换过程使用带宽。 但带宽是否需要事务转换取决于连接的设备类型和设备树的拓扑。

带宽资源的最严重压力通常来自独占带宽的 USB 客户端驱动程序。 系统会先返回第一个处理基础上的带宽分配。 如果第一个 USB 驱动程序加载请求所有可用带宽，在更高版本时将加载的 USB 驱动程序将获取所有其设备的任何带宽。 此操作时，系统不能配置设备，并且无法枚举它。 因为它通常不是很明显，枚举失败的原因，这可能导致不良用户体验。

有时，客户端驱动程序将用完可用带宽的高速中断传输。 但最常见的情况下，到目前为止，是，客户端驱动程序，它为同步传输，分配过多带宽然后未能释放及时的带宽。 系统会保留已分配的带宽，直到请求它的驱动程序 （通过打开另一个终结点），关闭其终结点或删除为其分配带宽的设备。 因此大容量传输永远不会枚举失败的原因，系统不会有保证的带宽分配的大容量传输。 但是，大容量传输设备的性能取决于为执行定期的设备分配多少带宽 (同步和中断) 传输。

USB 2.0 规范要求有零带宽终结点的默认接口设置同步设备。 这可确保任何带宽为设备保留，直到功能驱动程序打开的非默认接口，这也有助于防止枚举而导致的失败的请求过多的带宽在设备配置过程。 但是，它不会阻止客户端驱动程序配置其设备，从而阻止其他设备能够正常运行后分配过多带宽。

正确的带宽管理的关键是在完成同步传输系统中的每个 USB 设备必须提供包含同步终结点，每个接口的多个备用 (Alt) 设置和客户端驱动程序必须做出明智地使用这些Alt 设置。 客户端驱动程序应首先请求具有最高带宽的接口设置。 如果请求失败，客户端驱动程序应请求接口与越来越小带宽设置，直到请求成功。

例如，假设网络摄像头设备具有以下接口：

接口 0 (默认界面设置：使用默认设置中的非零值等时带宽没有终结点）

同步终结点 1： 最大数据包大小 = 0 字节

同步终结点 2： 最大数据包大小 = 0 字节

接口 0 Alt 设置 1

同步终结点 1： 最大数据包大小 = 256 个字节

同步终结点 2： 最大数据包大小 = 256 个字节

设置 2 接口 0 Alt

同步终结点 1： 最大数据包大小 = 512 个字节

同步终结点 2： 最大数据包大小 = 512 个字节

有关网络摄像头驱动程序配置的是网络摄像头进行初始化时使用的默认接口设置。 默认设置具有不等时的带宽，因此使用在初始化过程中的默认设置可避免网络摄像机可能会失败，若要枚举，因为失败的请求对等时的带宽的危险。

当客户端驱动程序已准备好进行同步传输时，它应尝试使用 Alt 设置 2，因为 Alt 设置 2 具有的最大的数据包大小。 如果请求失败，该驱动程序可以使第二次尝试，使用 Alt 设置 1。 由于 Alt 设置 1 要求较少的带宽，此请求可能成功，即使第一个请求失败。 多个 Alt 设置允许经过多次尝试，放弃前的驱动程序。

网络摄像头进入空闲状态后，它可以通过选择默认设置再一次到可用带宽池返回已分配的带宽。

从 Windows Vista 开始，用户可以查看 USB 控制器已通过检查控制器的属性在设备管理器分配的带宽。 选择控制器的属性，然后在高级选项卡下。此读取并不表示带宽 USB 集线器事务翻译已分配了多少。

报告的 USB 控制器的带宽使用量的设备管理器功能在 Windows XP 中无法正常工作。

 
## <a name="usb-transfer-and-packet-sizes"></a>USB 传输和数据包大小


本主题介绍在各种版本的 Windows 操作系统允许 USB 传输大小。

-   [最大传输大小](#maximum-transfer-size)
-   [最大数据包大小](#maximum-packet-size)
-   [对读取的传输缓冲区的最大数据包大小限制](#maximum-packet-size-restriction-on-read-transfer-buffers)
-   [使用短数据包分隔写入传输](#delimiting-write-transfers-with-short-packets)

### <a name="maximum-transfer-size"></a>最大传输大小


*最大传输大小*USB 驱动程序堆栈中指定硬编码限制。 很可能是传输大小下面这些限制将会因系统资源限制而失败。 若要避免这些类型的故障并确保跨所有版本的 Windows 兼容性，避免对 USB 传输使用大传输大小。

> **注意**  
>
> Windows XP、 Windows Server 2003 和更高版本中**最大传输大小**的成员[ **USBD\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)结构已过时。 USB 驱动程序堆栈将忽略中的值**最大传输大小**适用于组合键和非组合键的设备。
>
> 在 Windows 2000 中，初始化 USB 驱动程序堆栈**最大传输大小**到 USBD\_默认\_最大\_传输\_大小。 配置设备时，客户端驱动程序可以设置较小的值。 对于复合设备，只能更改每个函数的客户端驱动程序**最大传输大小**对于管道中的非默认接口设置。

USB 传输大小受到以下限制：

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
<th>Windows 7，Windows Vista</th>
<th>Windows XP、 Windows Server 2003</th>
<th>Windows 2000</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>控件</td>
<td><p>64k SuperSpeed 以及高速 (xHCI)</p>
<p>完整和低速度 (xHCI，EHCI，UHCI，OHCI) 为 4 千字节</p>
<p>有关 UHCI，默认终结点; 上的 4k对非默认的控制管道的 64k</p></td>
<td><p>64k 的高速 (EHCI)</p>
<p>完整和低速度 (EHCI，UHCI，OHCI) 为 4 千字节</p>
<p>有关 UHCI，默认终结点; 上的 4k64k 对非默认的控制管道 (UHCI)</p></td>
<td><p>64k 的高速 (EHCI)</p>
<p>完整和低速度 (EHCI，UHCI，OHCI) 为 4 千字节</p>
<p>有关 UHCI，默认终结点; 上的 4k64k 对非默认的控制管道 (UHCI)</p></td>
<td><p>默认终结点; 4 千字节64k 对非默认的控制管道 (OHCI)</p></td>
</tr>
<tr class="even">
<td>中断</td>
<td><p>SuperSpeed，高、 完全和低速度 (xHCI，EHCI、 UHCI、 OHCI) 为 4 MB</p></td>
<td><p>高、 完全和低速度 (EHCI，UHCI，OHCI) 为 4 MB</p></td>
<td>无限制</td>
<td><p>Undetermined(OHCI)</p></td>
</tr>
<tr class="odd">
<td>大容量</td>
<td><p>32 MB SuperSpeed (xHCI)</p>
<p>针对高和完整速度 (xHCI) 4 MB</p>
<p>针对高和完整速度 （EHCI 和 UHCI） 4 MB</p>
<p>256k 全速 (OHCI)</p></td>
<td><p>针对高和完整速度 （EHCI，UHCI） 4 MB</p>
<p>256k 用于全速 (OHCI)</p></td>
<td><p>针对高和完整速度 (EHCI) 3 MB</p>
<p>不确定 (UHCI)</p>
<p>256k 用于全速 (OHCI)</p></td>
<td><p>Undetermined(OHCI)</p></td>
</tr>
<tr class="even">
<td>等时</td>
<td><p>1024<em><strong>wBytesPerInterval</strong> (请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor" data-raw-source="[&lt;strong&gt;USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor)"> <strong>USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR</strong></a>) 为 SuperSpeed (xHCI)</p>
<p>1024</em> <strong>MaximumPacketSize</strong>高速度 (xHCI，EHCI)</p>
<p>256 * <strong>MaximumPacketSize</strong>完整速度 (xHCI，EHCI)</p>
<p>64 K 全速 （UHCI，OHCI）</p></td>
<td><p>1024 * <strong>MaximumPacketSize</strong>高速度 (EHCI)</p>
<p>256 * <strong>MaximumPacketSize</strong> for full-speed (EHCI)</p>
<p>64 K 全速 （UHCI，OHCI）</p></td>
<td><p>1024 * <strong>MaximumPacketSize</strong>的高速 (EHCI)</p>
<p>256 * <strong>MaximumPacketSize</strong>完整速度 (EHCI)</p>
<p>64 K 全速 （UHCI，OHCI）</p></td>
<td><p>64 K 全速 (OHCI)</p></td>
</tr>
</tbody>
</table>

 

限制使用的传输大小**最大传输大小**不直接影响设备多少带宽消耗。 客户端驱动程序必须将接口设置更改或限制中设置的最大数据包大小**MaximumPacketSize**的成员[ **USBD\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information).

### <a name="maximum-packet-size"></a>最大数据包大小


*最大数据包大小*由定义**wMaxPacketSize**终结点描述符字段。 客户端驱动程序可以控制到设备的选择接口请求中的 USB 数据包大小。 更改此值不会更改**wMaxPacketSize**在设备上。

在中[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)请求是[ **USBD\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)管道的结构。 在该结构中，

-   修改**MaximumPacketSize**的成员[ **USBD\_管道\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)结构。 将其设置为一个值小于或等于的值**wMaxPacketSize**当前接口设置的设备固件中定义。
-   设置 USBD\_PF\_更改\_最大\_中的数据包标志**PipeFlags**成员[ **USBD\_管道\_信息** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)结构。

有关选择界面设置的信息，请参阅[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)。

### <a name="maximum-packet-size-restriction-on-read-transfer-buffers"></a>对读取的传输缓冲区的最大数据包大小限制


当客户端驱动程序的读取的请求时，传输缓冲区必须是最大数据包大小的倍数。 甚至当驱动程序需要的数据不会早于最大数据包大小，它必须仍请求整个数据包。 当设备发送数据包不会早于最大大小 （短数据包） 时，则表示已完成传输。

**注意**  

较旧的控制器上的客户端驱动程序可以重写行为。 在中**TransferFlags**成员的数据传输[ **URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)，客户端驱动程序必须设置 USBD\_短\_传输\_确定标志。 该标志允许设备发送的数据包小于**wMaxPacketSize**。

在 xHCI 主控制器，USBD\_短\_传输\_忽略为大容量和中断终结点的确定。 EHCI 控制器上的简短的数据包传输不会导致错误条件。

EHCI 上托管控制器，USBD\_短\_传输\_确定将忽略为大容量和中断终结点。

UHCI 和 OHCI 上托管控制器，如果 USBD\_短\_传输\_确定未设置对于大容量或中断传输，短的数据包传输停止该终结点并进行传输返回的错误代码。

### <a name="delimiting-write-transfers-with-short-packets"></a>使用短数据包分隔写入传输


USB 驱动程序堆栈驱动程序不会施加数据包大小相同的限制时写入设备，它对从设备读取数据时。 某些客户端驱动程序必须进行频繁传输较少数量的控制数据，以便管理其设备。 它是不切实际限制传输到这种情况下统一大小的数据包数据。 因此，驱动程序堆栈不会分配任何特别的意义对数据包的大小小于终结点的最大大小的数据写入过程。 这允许客户端驱动程序即可进入任何大小小于或等于最大程度的多个 URBs 大型传输设备。

该驱动程序必须小于最大大小的数据包通过结束此传输或长度为零的数据包通过分隔传输结束。 传输不完整，直到该驱动程序将数据包发送小于*wMaxPacketSize*。 如果传输大小最大值的精确倍数，驱动程序必须发送零长度的分隔数据包，显式终止传输

分隔具有零长度的数据包数据传输，作为 USB 规范的要求是客户端驱动程序的责任。 USB 驱动程序堆栈不会自动生成这些数据包。

 
## <a name="delimiting-usb-data-transfers-with-packets-smaller-than-wmaxpacketsize"></a>分隔 USB 数据传输与数据包数小于 wMaxPacketSize


兼容的 USB 2.0/1.1 驱动程序必须传输数据包的最大大小 (*wMaxPacketSize*) 然后结束通过小于最大大小的数据包的传输或传输结束分隔通过长度为零数据包。 传输不完整，直到该驱动程序将数据包发送小于*wMaxPacketSize*。 如果传输大小最大值的精确倍数，驱动程序必须发送零长度的分隔数据包，显式终止传输

分隔具有零长度的数据包数据传输，所需的 USB 规范，负责的设备驱动程序。 系统 USB 堆栈不会自动生成这些数据包。


 




