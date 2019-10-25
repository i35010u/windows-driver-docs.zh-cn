---
Description: 本主题介绍客户端驱动程序的最佳实践，以便将 URB 分配、构建和发送到 Windows 8 随附的 USB 驱动程序堆栈。
title: 最佳做法-使用 URBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3127c45b6e63e21e91c324152fcfff17db32b26a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843200"
---
# <a name="best-practices-using-urbs"></a>最佳做法：使用 URBs


本主题介绍客户端驱动程序的最佳实践，以便将 URB 分配、构建和发送到 Windows 8 随附的 USB 驱动程序堆栈。

Windows 8 提供了一个新的 USB 驱动程序堆栈，用于支持通用串行总线（USB）3.0 设备。 新的 USB 3.0 驱动程序堆栈根据 USB 3.0 规范实现多种新功能。 此外，驱动程序堆栈还包含其他功能，使客户端驱动程序能够有效地执行常见任务。 例如，新的驱动程序堆栈接受链式 MDLs，以允许客户端驱动程序在物理内存中不连续的页中发送传输缓冲区。

在客户端驱动程序可以使用适用于 Windows 8 的 USB 驱动程序堆栈的新功能之前，驱动程序必须向 Windows 为设备加载的基础 USB 驱动程序堆栈自行注册。 若要注册客户端驱动程序，请调用[**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)并指定*协定版本*。 如果客户端驱动程序打算在 Windows 8 上生成、运行和使用改进和新功能，则客户端合同版本是 USBD\_客户端\_协定\_版本\_602。

对于 USBD\_客户端\_合约\_版本\_602 版客户端驱动程序，USB 驱动程序堆栈假定客户端驱动程序符合以下规则集：

-   [不要通过使用陈旧或无效的管道句柄发送 i/o 请求](#do-not-send-io-requests-by-using-stale-or-invalid-pipe-handles)
-   [通过在 Windows 8 中调用分配例程来分配 URBs](#allocate-urbs-by-calling-allocation-routines-in-windows8)
-   [不要重复使用与挂起的请求相关联的活动 URBs](#do-not-reuse-active-urbs-associated-with-pending-requests)
-   [对于高速和 SuperSpeed 同步传输，不要使用大于8的轮询周期](#do-not-use-polling-period-greater-than-8-for-high-speed-and-superspeed-isochronous-transfers)
-   [请确保每帧数据包数量为多个数据包的同步数据包数](#make-sure-that-the-number-of-isochronous-packets-that-is-a-multiple-of-number-of-packets-per-frame)
-   [在记录的 IRQL 级别调用例程](#call-the-routine-at-the-documented-irql-level)
-   [相关主题](#related-topics)

USB 驱动程序堆栈对收到的请求执行验证，并尽可能处理冲突。 否则，可能会导致未定义的行为。

## <a name="do-not-send-io-requests-by-using-stale-or-invalid-pipe-handles"></a>不要通过使用陈旧或无效的管道句柄发送 i/o 请求


客户端驱动程序*不得使用陈旧*的管道句柄将 i/o 请求发送到 USB 驱动程序堆栈。 *陈旧的管道句柄*指的是在请求中获得的管道句柄，用于选择配置、接口或不再在设备中选择的备用设置。 若要避免陈旧的管道句柄，每次客户端驱动程序选择配置或接口时，驱动程序必须刷新其管道句柄缓存（通常存储在设备上下文中）。 某些争用条件也可能导致陈旧的管道句柄。 例如，客户端驱动程序使用所选接口上的管道句柄发送 i/o 请求。 请求完成之前，客户端驱动程序将选择不使用与使用中的管道句柄关联的相同终结点的备用设置。 这两个挂起的请求都可能导致管道句柄无效的争用情况。

## <a name="allocate-urbs-by-calling-allocation-routines-in-windows8"></a>通过在 Windows 8 中调用分配例程来分配 URBs


Windows 8 提供了用于分配、构建和释放 USB 请求块（URBs）的新例程。 若要分配 URBs，Windows 驱动模型（WDM）客户端驱动程序必须始终使用下表中所示的新例程：

-   [**USBD\_UrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)
-   [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)
-   [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)
-   [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)
-   [**USBD\_UrbFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree)
-   [**USBD\_AssignUrbToIoStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)

前面列表中的例程可能会将不透明的 URB 上下文附加到分配的 URB，以便改进跟踪和处理。 客户端驱动程序无法查看或修改 URB 上下文的内容。 有关 Windows 8 中的 URB 分配的详细信息，请参阅[分配和生成 URBs](how-to-add-xrb-support-for-client-drivers.md)。

如果 Windows 驱动程序框架（WDF）客户端驱动程序在注册过程中将其版本标识为 USBD\_客户端\_协定\_版本\_602，**请参阅 USB**驱动程序堆栈要求客户端驱动程序通过调用新的**WdfUsbTargetDeviceCreateUrb**为 URB 分配内存。

## <a name="do-not-reuse-active-urbs-associated-with-pending-requests"></a>不要重复使用与挂起的请求相关联的活动 URBs


如果 USB 驱动程序堆栈检测到在与 URB 关联的请求之前已重新提交的活动 URB，则该堆栈会有意检查错误。 只要请求处于挂起状态，并且尚未调用客户端驱动程序的 IRP 完成例程，URB 就会处于活动状态。 不要在活动的 URB 上执行以下任务。

-   不要为另一*请求重新提交*活动的 URB （将 URB 与其他 IRP 相关联）。
-   请勿*修改活动*URB 的内容。
-   不要*释放活动*的 URB。

在调用客户端驱动程序的完成例程之后，驱动程序可以在完成例程内针对特定类型的请求重新提交 URBs。 以下规则适用于 resubmissions：

-   对于除了选择配置请求以外的任何类型的请求，客户端驱动程序不得重复使用 URB 分配给[**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild) 。
-   客户端驱动程序不得重复使用由[**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)为任何类型的请求分配的 URB，而不是选择接口请求来选择接口中的相同替代设置。 有关示例，请参阅**USBD\_SelectInterfaceUrbAllocateAndBuild**中的 "备注"。
-   [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)分配的 URB 必须仅对同步传输请求重复使用。 相反，为其他类型的 i/o 请求（控制、批量或中断）分配的 URB 不能用于同步请求。

    例如，客户端驱动程序为批量传输请求分配并生成[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构。 客户端驱动程序还想要将数据发送到设备中的同步终结点。 大容量传输请求完成后，客户端驱动程序*不得为同步请求重新格式化*并提交 URB。 这是因为与同步请求关联的 URB 的长度可变，具体取决于数据包的数量。 此外，数据包还需要在帧边界上启动和结束。 分配的 URB （用于大容量传输）可能不适合同步传输所需的缓冲区布局，请求可能会失败。

-   不能对同步、选择配置或选择接口请求重复使用[**USBD\_UrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)分配的 URB。 可以重复使用 URB 来选择 NULL 配置，以禁用设备中所选的配置。 URB 不得处于活动状态，并且客户端驱动程序必须通过调用[**UsbBuildSelectConfigurationRequest**](https://docs.microsoft.com/previous-versions/ff538968(v=vs.85))宏并在*ConfigurationDescriptor*参数中传递 NULL 来重新设置 URB 的格式。
-   在重新提交 URB 之前，客户端驱动程序必须使用为请求类型定义的适当**UsbBuildXxx**宏来重新设置 URB 的格式。 驱动程序需要设置 URB 的格式，这一点很重要，因为 USB stack 可能已更改了它的某些内容。

    例如，假定驱动程序调用[**UsbBuildInterruptOrBulkTransferRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildinterruptorbulktransferrequest)来初始化大容量传输请求的 URB （请参阅[ **\_URB\_批量\_或\_中断\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_bulk_or_interrupt_transfer)）。 如果驱动程序将[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的**TransferBufferMDL**成员初始化为 NULL，则 USB 驱动程序堆栈将使用中指定的**TransferBuffer**传输缓冲区来与设备交换数据，而不是使用 MDL。 但是，在内部，USB 驱动程序堆栈可能会创建一个 MDL，并在**TransferBufferMDL**中存储一个指向 mdl 的指针，并使用 MDL 将数据沿堆栈向下传递。 即使 USB 驱动程序堆栈释放 MDL 内存，当客户端驱动程序在完成例程中处理 URB 时， **TransferBufferMDL**可能不会为 NULL。 若要确保 URB 的成员的格式正确，驱动程序必须再次调用**UsbBuildInterruptOrBulkTransferRequest**来重新格式化 URB，然后再提交请求。

## <a name="do-not-use-polling-period-greater-than-8-for-high-speed-and-superspeed-isochronous-transfers"></a>对于高速和 SuperSpeed 同步传输，不要使用大于8的轮询周期


USB 驱动程序堆栈支持高速和 SuperSpeed 同步管道，轮询周期数为1、2、4或8。 客户端驱动程序不能将 IO 发送到周期大于8的终结点。 这样做可能会导致错误检测。

## <a name="make-sure-that-the-number-of-isochronous-packets-that-is-a-multiple-of-number-of-packets-per-frame"></a>请确保每帧数据包数量为多个数据包的同步数据包数


对于高速和 SuperSpeed 同步传输，每帧的同步数据包数将按 8/轮询周期计算。 客户端驱动程序必须确保在 URB 中指定的**NumberOfPackets**值（请参阅[ **\_URB\_ISOCH\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_isoch_transfer)）为每帧的数据包数倍数。

USB 驱动程序堆栈不支持按同步传输 URBs，其中**NumberOfPackets**不是每个帧的数据包数的倍数。

## <a name="call-the-routine-at-the-documented-irql-level"></a>在记录的 IRQL 级别调用例程


如果将客户端驱动程序注册到 USBD\_客户端的客户端驱动程序\_协定\_版本\_602 作为协定版本，则 USB 驱动程序堆栈会假定客户端驱动程序已在相应的 IRQL 级别发送请求。 如果客户端驱动程序在调度\_级别发送请求，则应在被动\_级别发送请求。 收到请求后，在某些情况下，USB 驱动程序堆栈会验证 IRQL 值并导致请求失败。 但在其他情况下，USB 驱动程序堆栈可能会生成错误检查。

## <a name="related-topics"></a>相关主题
[向 USB 设备发送请求](communicating-with-a-usb-device.md)  



