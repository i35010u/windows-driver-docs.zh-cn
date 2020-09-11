---
description: 有关 USB 客户端驱动程序如何可以分配、构建 URBs 并将其提交到 USB 驱动程序堆栈的信息。
title: USB 请求块 (URB)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15b2feb83f83813fe9edb425d5fa821961df2821
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009879"
---
# <a name="usb-request-blocks-urbs"></a>USB 请求块 (URB)


本部分介绍 (URB 的 USB 请求块) ，并提供有关 USB 客户端驱动程序如何使用 Windows 驱动模型 (WDM) 例程来分配、构建 URBs 并将其提交到 USB 驱动程序堆栈的信息。

通用串行总线 (USB) 客户端驱动程序无法直接与其设备通信。 相反，客户端驱动程序创建请求并将其提交到 USB 驱动程序堆栈进行处理。 在每个请求中，客户端驱动程序提供长度可变的数据结构，称为 *USB 请求块 (URB) *。 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构描述请求的详细信息，还包含有关已完成请求的状态的信息。 客户端驱动程序通过 URBs 执行所有设备特定的操作，包括数据传输。 在将 URB 提交到 USB 驱动程序堆栈之前，客户端驱动程序必须用该请求的相关信息对其进行初始化。 对于某些类型的请求，Microsoft 提供了 helper 例程和宏，用于分配 **URB** 结构并使用客户端驱动程序提供的详细信息填充 **URB** 结构的必要成员。

每个 URB 都从标准固定大小的标头 ([** \_ URB \_ 标**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_header)头开始，) 其用途是标识所请求操作的类型。 ** \_ URB \_ 标头**的**Length**成员指定 URB 的大小（以字节为单位）。 **函数**成员（必须是一系列系统定义的 URB \_ 函数 \_ XXX 常量）决定所请求的操作的类型。 例如，在进行数据传输的情况下，此成员指示传输类型。 函数代码 URB \_ 函数 \_ 控制 \_ 传输、URB \_ 函数 \_ BULK \_ 或 \_ 中断 \_ 传输，URB \_ 函数 \_ ISOCH \_ 传输分别指示控件、大容量/中断和同步传输。 USB 驱动程序堆栈使用 **Status** 成员返回 USB 特定状态代码。

若要提交 URB，客户端驱动程序将使用 [**IOCTL \_ 内部 \_ USB \_ submit \_ URB**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) 请求，该请求通过 i/o 请求数据包 (irp) 类型 [**irp \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)发送到设备。

USB 驱动程序堆栈处理完 URB 后，驱动程序堆栈会使用[**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的**Status**成员返回特定于 USB 的状态代码。

**注意**   KMDF 和 UMDF 驱动程序开发人员应使用各自的框架接口与 USB 设备进行通信。 有关详细信息，请参阅使用 [Usb 设备](../wdf/working-with-usb-devices.md) 获取 KMDF 驱动程序和 [在 UMDF 中使用 usb 接口](../wdf/working-with-usb-interfaces-in-umdf-1-x-drivers.md)。 这些主题讨论了用于 USB 设备通信的底层 WDM 驱动程序接口。

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
<td><p><a href="how-to-add-xrb-support-for-client-drivers.md" data-raw-source="[Allocating and Building URBs](how-to-add-xrb-support-for-client-drivers.md)">分配和构建 URB</a></p></td>
<td><p>本主题介绍在将请求发送到 Microsoft 提供的 USB 驱动程序堆栈之前，USB 客户端驱动程序如何使用 Windows 驱动模型 (WDM) 驱动程序例程来分配 URB 并设置其格式。</p></td>
</tr>
<tr class="even">
<td><p><a href="send-requests-to-the-usb-driver-stack.md" data-raw-source="[How to Submit an URB](send-requests-to-the-usb-driver-stack.md)">如何提交 URB</a></p></td>
<td><p>本主题介绍将已初始化的 URB 提交到 USB 驱动程序堆栈以处理特定请求所需的步骤。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-client-driver-contract-in-windows-8.md" data-raw-source="[Best Practices: Using URBs](usb-client-driver-contract-in-windows-8.md)">最佳做法：使用 URB</a></p></td>
<td><p>本主题介绍客户端驱动程序的最佳实践，以便将 URB 分配、构建和发送到 Windows 8 随附的 USB 驱动程序堆栈。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 驱动程序开发指南](usb-driver-development-guide.md)