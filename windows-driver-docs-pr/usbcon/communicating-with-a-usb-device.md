---
Description: 有关 USB 客户端驱动程序可以分配、 生成和提交 URBs 到 USB 驱动程序堆栈的信息。
title: USB 请求块 (URBs)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05565efe50edaf7600f4e78de377550d638315f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378359"
---
# <a name="usb-request-blocks-urbs"></a>USB 请求块 (URBs)


本部分中描述的 USB 请求块 (URB)，并提供有关 USB 客户端驱动程序如何使用 Windows 驱动程序模型 (WDM) 例程分配、 生成，并将 URBs 提交到 USB 驱动程序堆栈的信息。

通用串行总线 (USB) 客户端驱动程序无法直接通信与其设备。 相反，客户端驱动程序创建请求，并将其提交给 USB 驱动程序堆栈进行处理。 在每个请求，客户端驱动程序提供名的长度可变的数据结构*USB 请求块 (URB)* 。 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)结构介绍了请求的详细信息，还包括已完成请求的状态信息。 客户端驱动程序执行所有特定于设备的操作，包括数据传输，通过 URBs。 客户端驱动程序必须初始化 URB 与提交到 USB 驱动程序堆栈之前有关请求的信息。 对于某些类型的请求，Microsoft 提供的帮助器例程和分配的宏**URB**结构，并填充的所需成员**URB**结构与提供的客户端详细信息驱动程序。

每个 URB 开头固定大小的标准标头 ([ **\_URB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_header)) 其用途是确定的请求操作的类型。 **长度**的成员 **\_URB\_标头**指定的大小，以字节为单位 URB。 **函数**成员，必须是一个系列的系统定义 URB\_函数\_XXX 常量确定的请求的操作的类型。 例如，对于数据传输，此成员表示传输的类型。 函数代码 URB\_函数\_控制\_传输、 URB\_函数\_大容量\_或者\_中断\_传输和 URB\_函数\_ISOCH\_传输分别指示控制、 大容量/中断和同步传输。 使用 USB 驱动程序堆栈**状态**成员以返回特定于 USB 的状态代码。

若要提交 URB，客户端驱动程序，请使用[ **IOCTL\_内部\_USB\_提交\_URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)的方式发送到设备的请求类型的 I/O 请求数据包 (IRP) 的[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)。

后 USB 驱动程序堆栈是处理 URB，使用驱动程序堆栈**状态**的成员[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)结构，以返回特定于 USB 的状态代码。

**请注意**  KMDF 和 UMDF 驱动程序开发人员应使用各自的框架接口用于与 USB 设备进行通信。 有关详细信息，请参阅[使用 USB 设备](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-devices)KMDF 驱动程序和[使用 USB 接口在 UMDF](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers)。 这些主题介绍如何使用 USB 设备之间的基础 WDM 驱动程序接口。

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
<td><p><a href="how-to-add-xrb-support-for-client-drivers.md" data-raw-source="[Allocating and Building URBs](how-to-add-xrb-support-for-client-drivers.md)">分配和构建 URBs</a></p></td>
<td><p>本主题介绍 USB 客户端驱动程序如何使用 Windows 驱动程序模型 (WDM) 驱动程序例程来分配和设置 URB 格式之前将请求发送到由 Microsoft 提供的 USB 驱动程序堆栈。</p></td>
</tr>
<tr class="even">
<td><p><a href="send-requests-to-the-usb-driver-stack.md" data-raw-source="[How to Submit an URB](send-requests-to-the-usb-driver-stack.md)">如何提交 URB</a></p></td>
<td><p>本主题介绍提交初始化的 URB USB 驱动程序堆栈处理特定请求所需的步骤。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-client-driver-contract-in-windows-8.md" data-raw-source="[Best Practices: Using URBs](usb-client-driver-contract-in-windows-8.md)">最佳做法：使用 URBs</a></p></td>
<td><p>本主题介绍用于分配、 生成和发送到 Windows 8 附带的 USB 驱动程序堆栈 URB 的客户端驱动程序的最佳做法。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



