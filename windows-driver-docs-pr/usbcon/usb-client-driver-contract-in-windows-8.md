---
Description: 本主题介绍用于分配、 生成和发送到 Windows 8 附带的 USB 驱动程序堆栈 URB 的客户端驱动程序的最佳做法。
title: 最佳做法-使用 URBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3c8d2bbb6bed330ef9f537e07f9fd991638b7bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369526"
---
# <a name="best-practices-using-urbs"></a>最佳做法：使用 URB


本主题介绍用于分配、 生成和发送到 Windows 8 附带的 USB 驱动程序堆栈 URB 的客户端驱动程序的最佳做法。

Windows 8 中包含新的 USB 驱动程序堆栈，以支持通用串行总线 (USB) 3.0 的设备。 新的 USB 3.0 驱动程序堆栈实现几个新功能，根据 USB 3.0 规范。 此外，驱动程序堆栈包括其他功能，使客户端驱动程序即可有效地执行常见任务。 例如，新的驱动程序堆栈接受链接在一起-MDLs，允许客户端驱动程序将在物理内存不连续的页中发送的传输缓冲区。

客户端驱动程序可用于 Windows 8 的 USB 驱动程序堆栈的新功能之前，该驱动程序必须注册本身与基础 Windows 设备中加载的 USB 驱动程序堆栈。 若要注册客户端驱动程序，请调用[ **USBD\_CreateHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_createhandle) ，并指定*协定版本*。 如果客户端驱动程序用于生成、 运行和在 Windows 8 上使用的改进和新功能，客户端协定版本是 USBD\_客户端\_协定\_版本\_602。

有关 USBD\_客户端\_协定\_版本\_602 版客户端驱动程序，USB 驱动程序堆栈假定客户端驱动程序符合以下规则集：

-   [不发送使用过期或无效的管道句柄的 I/O 请求](#do-not-send-io-requests-by-using-stale-or-invalid-pipe-handles)
-   [通过在 Windows 8 中调用的分配例程分配 URBs](#allocate-urbs-by-calling-allocation-routines-in-windows8)
-   [不要重复使用与挂起的请求相关联的 active URBs](#do-not-reuse-active-urbs-associated-with-pending-requests)
-   [使用轮询时间不大于 8 的高速和 SuperSpeed 同步传输](#do-not-use-polling-period-greater-than-8-for-high-speed-and-superspeed-isochronous-transfers)
-   [请确保每个框架的数据包数的倍数的同步数据包数](#make-sure-that-the-number-of-isochronous-packets-that-is-a-multiple-of-number-of-packets-per-frame)
-   [在有案可稽的 IRQL 级别调用该例程](#call-the-routine-at-the-documented-irql-level)
-   [相关主题](#related-topics)

USB 驱动程序堆栈上接收的请求执行验证并处理只要有可能的违规行为。 如果不这样做可能会导致未定义的行为。

## <a name="do-not-send-io-requests-by-using-stale-or-invalid-pipe-handles"></a>不发送使用过期或无效的管道句柄的 I/O 请求


客户端驱动程序必须*不*使用过时的管道句柄将 I/O 请求发送到 USB 驱动程序堆栈。 一个*过时的管道句柄*引用中选择一个配置、 接口或替代设置不能再在设备中选择的请求获得的管道句柄。 若要避免过时的管道句柄，每次客户端驱动程序选择一个配置或接口时，该驱动程序必须刷新其缓存 （通常存储在设备上下文） 的管道句柄。 某些争用情况也可能导致过时的管道句柄。 例如，客户端驱动程序发送的 I/O 请求所选接口上使用的管道句柄。 在请求完成之前，客户端驱动程序选择不使用相同的终结点与正在使用的管道句柄关联的备用设置。 这两个挂起的请求可能会导致争用条件进行的管道句柄无效。

## <a name="allocate-urbs-by-calling-allocation-routines-in-windows8"></a>通过在 Windows 8 中调用的分配例程分配 URBs


Windows 8 提供新的分配、 生成和发布 USB 请求块 (URBs) 的例程。 若要分配 URBs，Windows 驱动程序模型 (WDM) 客户端驱动程序必须始终使用下面的列表中所示的新例程：

-   [**USBD\_UrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urballocate)
-   [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_isochurballocate)
-   [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)
-   [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)
-   [**USBD\_UrbFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urbfree)
-   [**USBD\_AssignUrbToIoStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)

上述列表中的例程可能会将不透明的 URB 上下文附加到已分配 URB，以便提高跟踪和处理。 客户端驱动程序不能查看或修改 URB 上下文的内容。 有关 Windows 8 中 URB 分配的详细信息，请参阅[Allocating 和构建 URBs](how-to-add-xrb-support-for-client-drivers.md)。

如果 Windows 驱动程序框架 (WDF) 的客户端驱动程序，用于标识其版本为 USBD\_客户端\_协定\_版本\_602 在注册过程中的 (请参阅**WdfUsbTargetDeviceCreateWithParameters**)，USB 驱动程序堆栈要求分配内存来存放 URB 通过调用新的客户端驱动程序**WdfUsbTargetDeviceCreateUrb**。

## <a name="do-not-reuse-active-urbs-associated-with-pending-requests"></a>不要重复使用与挂起的请求相关联的 active URBs


如果它检测到的活动在请求之前重新提交的 URB 与关联 URB USB 驱动程序堆栈故意错误检查。 只要请求处于挂起状态，并且尚未调用客户端驱动程序的 IRP 完成例程，URB 处于活动状态。 不要在 active URB 上执行以下任务。

-   不要*不*重新提交另一个请求 （关联与另一个 IRP URB） active URB。
-   不要*不*修改 active URB 的内容。
-   不要*不*免费 active URB。

客户端驱动程序的完成例程调用之后，驱动程序可以重新提交 URBs 某些类型的请求内完成例程。 以下规则适用于重新提交：

-   客户端驱动程序不重复使用分配的 URB [ **USBD\_SelectConfigUrbAllocateAndBuild** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)为任何类型的选择相同的选择配置请求之外的请求配置。
-   客户端驱动程序不重复使用分配的 URB [ **USBD\_SelectInterfaceUrbAllocateAndBuild** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)为任何类型的选择相同的选择接口请求之外的请求在接口中的替代设置。 有关示例，请参阅备注中的**USBD\_SelectInterfaceUrbAllocateAndBuild**。
-   由分配 URB [ **USBD\_IsochUrbAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_isochurballocate)必须仅针对同步传输请求重复使用。 相反，对于其他类型的 I/O 请求 （控件、 大容量或中断） 分配 URB 不必须用于同步请求。

    例如，客户端驱动程序分配，并生成[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)的大容量传输请求的结构。 客户端驱动程序还想要将数据发送到设备中的同步终结点。 客户端驱动程序的大容量传输请求完成后，必须*不*重新格式化并提交同步请求 URB。 这是因为一个同步请求，与关联 URB 具有可变长度根据数据包的数量。 此外，数据包都需要开始和结束的框架边界。 （适用于大容量传输中） 已分配的 URB 可能并不符合所需的同步传输的缓冲区布局，则请求可能会失败。

-   由分配 URB [ **USBD\_UrbAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urballocate)不能将重复使用的同步、 选择配置或选择接口请求。 URB 可用于选择要禁用所选的配置的设备中的 NULL 配置重复使用。 URB 必须不处于活动状态和客户端驱动程序必须通过调用格式化 URB [ **UsbBuildSelectConfigurationRequest** ](https://docs.microsoft.com/previous-versions/ff538968(v=vs.85))宏和中传递 NULL *ConfigurationDescriptor*参数。
-   然后重新提交 URB，客户端驱动程序必须通过重新格式化 URB 使用相应**UsbBuildXxx**为请求的类型定义的宏。 由于 USB 堆栈可能会更改其内容的一些驱动程序来设置格式 URB 至关重要。

    例如，假设一个驱动程序调用[ **UsbBuildInterruptOrBulkTransferRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbbuildinterruptorbulktransferrequest)初始化大容量传输请求 URB (请参阅[  **\_URB\_大容量\_或者\_中断\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_bulk_or_interrupt_transfer))。 如果该驱动程序初始化**TransferBufferMDL**的成员[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)结构为 NULL，USB 驱动程序堆栈使用指定的传输缓冲区**TransferBuffer**，以与设备而不是 MDL 交换数据。 但是，在内部，USB 驱动程序堆栈可能创建 MDL，存储指向中 MDL **TransferBufferMDL**，并使用 MDL 堆栈的下层的数据传递。 即使 USB 驱动程序堆栈释放 MDL 内存，也是如此**TransferBufferMDL**可能不能为 NULL，当客户端驱动程序正在处理中完成例程 URB 时。 若要确保正确设置格式的 URB 成员，该驱动程序必须调用**UsbBuildInterruptOrBulkTransferRequest**再次以重新 URB 提交请求之前设置的格式

## <a name="do-not-use-polling-period-greater-than-8-for-high-speed-and-superspeed-isochronous-transfers"></a>使用轮询时间不大于 8 的高速和 SuperSpeed 同步传输


USB 驱动程序堆栈支持高速度和 SuperSpeed 等时管道以 1、 2、 4 或 8 轮询周期数。 客户端驱动程序必须发送到终结点的周期为大于 8 的 IO。 执行此操作可能会导致出现 bugcheck。

## <a name="make-sure-that-the-number-of-isochronous-packets-that-is-a-multiple-of-number-of-packets-per-frame"></a>请确保每个框架的数据包数的倍数的同步数据包数


对于高速度和 SuperSpeed 同步传输，每个框架等时数据包数计算为 8 / 轮询段。 客户端驱动程序必须确保**NumberOfPackets** URB 中指定的值 (请参阅[  **\_URB\_ISOCH\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_isoch_transfer)) 的每一帧的数据包数的倍数。

USB 驱动程序堆栈不支持在其中同步传输 URBs **NumberOfPackets**不是每个框架的数据包数的倍数。

## <a name="call-the-routine-at-the-documented-irql-level"></a>在有案可稽的 IRQL 级别调用该例程


如果您的客户端驱动程序注册 USBD\_客户端\_协定\_版本\_作为协定版本 602，USB 驱动程序堆栈假定客户端驱动程序发送请求在适当的 IRQL 级别。 如果客户端驱动程序发送的请求在调度\_级别，应在被动发送\_级别。 收到请求后，在某些情况下，USB 驱动程序堆栈验证 IRQL 值，并使请求失败。 但是，在其他情况下，USB 驱动程序堆栈可能会生成错误检查。

## <a name="related-topics"></a>相关主题
[将请求发送到 USB 设备](communicating-with-a-usb-device.md)  



