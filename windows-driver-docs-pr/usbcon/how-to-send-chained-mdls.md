---
Description: 在本主题中，你将了解有关 USB 驱动程序堆栈中链式 MDLs 功能的信息，以及客户端驱动程序如何以 MDL 结构链形式发送传输缓冲区。
title: 如何发送链接的 MDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75581208dab5c66926122ac6cf28662236e4177a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837546"
---
# <a name="how-to-send-chained-mdls"></a>如何发送链接的 MDL


在本主题中，你将了解有关 USB 驱动程序堆栈中链式 MDLs 功能的信息，以及客户端驱动程序如何以[**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)结构链形式发送传输缓冲区。

大多数 USB 主机控制器都需要传输缓冲区，这一点几乎是连续的。 "虚拟连续" 表示缓冲区可以在页面的任意位置开始和结束，但缓冲区的其余部分必须在页面边界上开始和结束。 许多 USB 客户端驱动程序都可以满足这一要求。 但是，对于某些客户端驱动程序（特别是那些需要在缓冲区中添加或删除额外数据的驱动程序），为传输缓冲区分配虚拟连续内存并不可取。

例如，假设有三个驱动程序的网络堆栈、网络协议驱动程序、中间驱动程序和微型端口驱动程序。 协议驱动程序启动传输并将数据包发送到堆栈中的下一个驱动程序：中间驱动程序。 中间驱动程序想要将自定义标头（包含在单独的内存块中）添加到数据包。 中间驱动程序会将该标头和收到的数据包发送到堆栈中的下一个驱动程序：微型端口驱动程序。 小型端口驱动程序与 USB 驱动程序堆栈的接口，因此必须准备一个近乎连续的传输缓冲区。 若要创建此类缓冲区，微型端口驱动程序会分配一个较大的缓冲区，添加自定义标头，然后复制负载。 由于负载通常很大，因此复制整个负载会对性能产生重大影响。

客户端驱动程序可以通过以*内存描述符列表*（MDLs）的链形式发送传输缓冲区来克服对性能的影响。 Windows 8 中的新 USB 驱动程序堆栈可以接受来自客户端驱动程序的连锁 MDL （请参阅[**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)）。 通过提供链式 MDL，客户端驱动程序可在内存中引用不连续的页，而不是执行无关的复制操作。 此功能消除了对缓冲区的数量、大小和对齐的限制，从而允许在物理内存中分段传输缓冲区。

为了使用链式 MDLs，客户端驱动程序必须检测由 Windows 加载的基础 USB 驱动程序堆栈是否支持该功能，然后按正确的顺序生成 MDLs 链。

### <a name="prerequisites"></a>必备条件

仅限大容量、同步和中断传输支持连锁 MDL 功能。 在查询链式 MDL 功能之前，请确保客户端驱动程序具有用于驱动程序注册到 USB 驱动程序堆栈的 USBD 句柄。 若要创建 USBD 句柄，请调用[**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)。通常，客户端驱动程序会在其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中创建 USBD 句柄。

可以在客户端驱动程序的[**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)处理程序中或稍后随时查询链式 MDL 功能。 客户端驱动程序不能在其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中查询此功能。

<a name="instructions"></a>说明
------------

1.  调用[**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))例程来确定 USB 驱动程序堆栈是否支持链式 MDLs 功能。 若要查询该功能，请将 UsbCapabilityChainedMdls 指定为 GUID。 将*OutputBuffer*参数设置为 NULL，将*OutputBufferSize*参数设置为0。
2.  检查[**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))返回的 NTSTATUS 值并计算结果。 如果例程成功完成，则支持链接的 MDLs 功能。 任何其他值表示不支持此功能。
3.  创建 MDLs 的链。 每个[**mdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)都具有指向另一个**mdl**的**下**一个指针。

    驱动程序可以通过手动设置**下一个**指针来构建链 MDL。

    在前面的示例中，协议驱动程序将数据包作为 MDL 发送。 中间驱动程序可以创建另一个 MDL，该[**MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)引用带有标头数据的内存块。 若要创建链，中间驱动程序可以使标头 MDL 的**下一个**指针指向从协议驱动程序收到的 MDL。 然后，中间驱动程序可以将两个 MDLs 的链转发到微型端口驱动程序，该驱动程序为请求提供对 URB 中链式 MDL 的引用并将请求提交到 USB 驱动程序堆栈。 有关详细信息，请参阅[Using MDLs](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-mdls)。

4.  为使用链式 MDLs 的 i/o 请求生成 URB 时，请设置关联[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的**TransferBufferMDL**成员（如[ **\_URB\_BULK\_或\_中断\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_bulk_or_interrupt_transfer)或[ **\_URB\_ISOCH\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer)）到链中的第一个 MDL，并将**TransferBufferLength**设置为要传输的总字节数。 数据可能跨 MDL 链中的一个或多个 MDL 条目。

    在 Windows 8 中，添加了两种新类型的 URB 函数，使客户端驱动程序可以使用链式 MDLs 进行数据传输。 如果要使用此功能，请确保将 URB 标头的**Function**成员设置为以下 URB 函数之一：

    -   URB\_函数\_批量\_或\_中断\_使用\_链接\_MDL 传输\_
    -   URB\_函数\_ISOCH\_传输\_使用\_链接\_MDL

    有关这些 URB 函数的信息，请参阅[ **\_URB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_header)。

<a name="remarks"></a>备注
-------

有关查询基础 USB 驱动程序堆栈以确定驱动程序堆栈是否可以接受链式 MDLs 的代码示例，请参阅[**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))。

## <a name="related-topics"></a>相关主题
[USB i/o 操作](usb-device-i-o.md)  



