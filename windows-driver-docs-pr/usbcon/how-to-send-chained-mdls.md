---
Description: 在本主题中，您将学习有关 USB 驱动程序堆栈，以及客户端驱动程序如何作为 MDL 结构链发送的传输缓冲区中的链接 MDLs 功能。
title: 如何发送链接的 MDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e9ffe07dbb30ff43144ace3f621dd55ae766265
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384587"
---
# <a name="how-to-send-chained-mdls"></a>如何发送链接的 MDL


在本主题中，您将学习有关 USB 驱动程序堆栈，并且如何客户端驱动程序可以发送的传输缓冲区作为链中的链接 MDLs 功能[ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414)结构。

大多数 USB 主控制器需要传输缓冲区是几乎连续。 缓冲区可以开始和结束页，但缓冲区的其余部分中的任意位置的几乎连续意味着必须开始和结束的页边界。 许多 USB 客户端驱动程序将能够满足该要求。 但是，对于某些客户端驱动程序，特别是那些需要添加或删除其他数据到或从缓冲区中，为传输缓冲区分配几乎连续内存不是更可取。

例如，考虑三个的驱动程序、 网络协议驱动程序、 中间驱动程序和微型端口驱动程序的网络堆栈。 协议驱动程序启动传输，并将数据包发送到堆栈中的下一步驱动程序： 中间驱动程序。 中间驱动程序想要添加自定义标头 （包含在单独的内存块） 数据包。 中间驱动程序将该标头和所接收的数据包发送到堆栈中的下一步驱动程序： 微型端口驱动程序。 微型端口驱动程序接口与 USB 驱动程序堆栈，并因此必须准备几乎连续传输缓冲区。 若要创建此类缓冲区，微型端口驱动程序分配较大的缓冲区，将添加自定义标头，，然后复制负载。 有效负载为通常较大，因为复制整个负载可以具有对性能的重大影响。

客户端驱动程序可以通过将作为链中发送的传输缓冲区来克服这种性能影响*内存描述符列表*(MDLs)。 在 Windows 8 中，新的 USB 驱动程序堆栈是可接受链接的 MDL (请参阅[ **MDL**](https://msdn.microsoft.com/library/windows/hardware/ff554414)) 从客户端驱动程序。 通过提供链接的 MDL，客户端驱动程序可以引用在内存中而不是执行无关的复制操作不连续的页。 功能中移除对数量、 大小和缓冲区，允许其进行分段的物理内存中的传输缓冲区的对齐方式的限制。

若要使用链接的 MDLs，客户端驱动程序必须检测是否基础的 USB 驱动程序堆栈，加载的 Windows，支持功能，然后生成 MDLs 链中正确的顺序。

### <a name="prerequisites"></a>先决条件

大容量等时，才支持连锁的 MDL 功能并将传输中断。 查询链接 MDL 功能之前，请确保您的客户端驱动程序具有与 USB 驱动程序堆栈的驱动程序的注册的 USBD 句柄。 若要创建 USBD 句柄，请调用[ **USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)。通常情况下，客户端驱动程序创建 USBD 句柄中的其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程。

您可以查询客户端驱动程序中的链接 MDL 功能[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)处理程序或任何时候更高版本。 客户端驱动程序必须查询的这一功能及其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程。

<a name="instructions"></a>说明
------------

1.  调用[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)例程，以确定 USB 驱动程序堆栈是否支持连锁的 MDLs 功能。 若要查询的该功能，请指定的 guid UsbCapabilityChainedMdls。 设置*OutputBuffer*为 NULL 的参数和*OutputBufferSize*参数设为 0。
2.  检查返回的 NTSTATUS 值[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)和评估结果。 如果成功完成例程，支持连锁的 MDLs 功能。 任何其他值指示不支持此功能。
3.  创建 MDLs 链。 每个[ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414)具有**下一步**指针指向另一个**MDL**。

    该驱动程序可以通过手动设置生成链 MDL**下一步**指针。

    在前面的示例中，协议驱动程序将作为 MDL 发送数据包。 中间驱动程序可以创建另一个[ **MDL** ](https://msdn.microsoft.com/library/windows/hardware/ff554414)引用与标头数据的内存块。 若要创建一个链，中间驱动程序可以指向标头 MDL**下一步**指向 MDL 来自协议驱动程序。 中间驱动程序然后可以将转发到微型端口驱动程序，它提供对中请求 URB 连锁 MDL 的引用，并将提交对 USB 驱动程序堆栈的请求的两个 MDLs 链。 有关详细信息，请参阅[使用 MDLs](https://msdn.microsoft.com/library/windows/hardware/ff565421)。

4.  有关使用的 I/O 请求链接 MDLs 生成 URB，时设置**TransferBufferMDL**关联的成员[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构 (如[ **\_URB\_大容量\_OR\_中断\_传输**](https://msdn.microsoft.com/library/windows/hardware/ff540352)或[  **\_URB\_ISOCH\_传输**](https://msdn.microsoft.com/library/windows/hardware/ff540414)) 到中的链，并设置第一个 MDL **TransferBufferLength**要传输的字节总数。 数据可能跨多个 MDL 链中的 MDL 条目。

    在 Windows 8 中，两个新类型的 URB 函数已添加，使客户端驱动程序以使用链接的 MDLs 进行数据传输。 如果你想要使用此功能，请确保该设置**函数**URB 标头的成员设置为下列 URB 函数之一：

    -   URB\_函数\_大容量\_或者\_中断\_传输\_USING\_CHAINED\_MDL
    -   URB\_函数\_ISOCH\_传输\_USING\_CHAINED\_MDL

    有关这些 URB 函数的信息，请参阅[  **\_URB\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff540409)。

<a name="remarks"></a>备注
-------

有关查询基础的 USB 驱动程序堆栈，以确定驱动程序堆栈是否可以接受链接的 MDLs 的代码示例，请参阅[ **USBD\_QueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh406230)。

## <a name="related-topics"></a>相关主题
[USB I/O 操作](usb-device-i-o.md)  



