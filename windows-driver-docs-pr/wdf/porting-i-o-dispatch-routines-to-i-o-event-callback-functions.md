---
title: 将 I/O 调度例程移植到 I/O 事件回调函数
description: 将 I/O 调度例程移植到 I/O 事件回调函数
ms.assetid: 0BD65185-C358-4E28-8E31-255AF8D77F93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab11ee720dae3b4eaef1b74a99848092dc871d7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379639"
---
# <a name="porting-io-dispatch-routines-to-io-event-callback-functions"></a>将 I/O 调度例程移植到 I/O 事件回调函数


WDM 驱动程序的 I/O 调度例程的核心将映射到 WDF 驱动程序的 I/O 事件回调函数。 然而，I/O 事件回调函数的几个重要方面与 WDM 驱动程序的 I/O 调度例程有所不同：

-   当框架调用 WDF 驱动程序的 I/O 事件回调时，回调在无法状态中收到的请求。 不能取消该请求，除非该驱动程序显式将其标记为可取消。
-   该驱动程序指定框架是否同步对 I/O 事件回调的调用，以便只有一个此类回调并发运行每个队列或每个设备对象，或是否在框架应用没有同步根本。 有关选择同步选项的详细信息，请参阅[使用自动同步](using-automatic-synchronization.md)。

这些差异意味着大多数 I/O 事件回调函数包含大大减少代码的访问进行同步，并避免出现争用情况比相应 WDM **DispatchXxx**例程。

同步过程中，除了 WDM 驱动程序的 I/O 之间的主要区别调度例程和驱动程序如何检索参数和它如何访问 I/O 缓冲区中的 WDF 驱动程序的 I/O 事件回调函数欺骗。

## <a name="parameters-for-io-requests"></a>I/O 请求的参数


根据请求 WDF 驱动程序处理，并配置其 I/O 队列的方式，驱动程序可能不需要分析作为 WDM 驱动程序的 I/O 请求的参数的类型执行操作。 框架将为读取、 写入和设备 I/O 控制请求时调用 I/O 事件回调 ([*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)， [ *EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)，[ *EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)， [ *EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control))，它提取最常使用的参数从 IRP 并将其作为参数传递给回调。 例如，框架将调用的驱动程序*EvtIoRead*回调的句柄 WDFREQUEST 对象和要读取的字节数。 如果该驱动程序不需要设备偏移量或排序键，它可以只需检索缓冲区从 WDFREQUEST 对象通过调用之一**WdfRequestRetrieveOutputXxx**方法; 它不需要检索其他参数。

在中**EvtIoDefault**回调，但是，框架仅将句柄传递到队列和请求对象的句柄。 因此，该驱动程序必须调用**WdfRequestGetParameters**若要获取的参数，包括请求的类型 (**WdfRequestTypeXxx**)。 [**WdfRequestGetParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)返回[ **WDF\_请求\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_parameters)结构，其中包含与传递的参数创建、 读取、 写入、 设备 I/O 控制或内部设备 I/O 控制请求。

## <a name="access-to-buffers-for-buffered-and-direct-io"></a>对缓冲区的缓冲和直接 I/O 访问权限


当框架收到请求时的 I/O 时，它会创建封装基础 WDM IRP WDFREQUEST 对象。 它然后排队 WDFREQUEST 对象，并最终将该驱动程序根据消息调度[调度规范](dispatching-methods-for-i-o-requests.md)队列。 该驱动程序使用 WDF 方法来检索参数和 I/O 请求的缓冲区。 驱动程序可以获取基础 WDM IRP 在任何时候通过调用[ **WdfRequestWdmGetIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)。

WDF 驱动程序可以支持 WDM 驱动程序，如[缓冲，直接或都不 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)。 驱动程序设置的支持对于每个设备对象的调用的 I/O 操作的类型[ **WdfDeviceInitSetIoType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)中[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)之前创建的设备对象的回调。 与不同的 WDM 驱动程序，但是，KMDF 驱动程序访问缓冲区中的相同方式是否它执行缓冲或直接 I/O，并为每个使用相同的方法。

尽管 WDF 驱动程序用于缓冲和直接 I/O，以相同的方式访问缓冲区，但它使用不同的方法来检索具体取决于 I/O 请求的类型的缓冲区。 以下部分介绍驱动程序处理每种类型的 I/O 请求的方式：

-   [创建请求](#create-requests)
-   [读取请求](#read-requests)
-   [写入请求](#write-requests)
-   [设备 I/O 控制请求](#device-io-control-requests)
-   [内部设备 I/O 控制请求](#internal-device-io-control-requests)

## <a name="create-requests"></a>创建请求


WDF 驱动程序可以处理创建请求 ([**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)) 在两种方式之一：

-   绕过队列，并改为提供[ *EvtDeviceFileCreate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调。
-   具有 framework 队列创建请求和实施[ *EvtIoDefault* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)回调以处理来自队列的此类请求。

有关处理文件的创建请求的详细信息，请参阅[Framework 文件对象](framework-file-objects.md#creating-or-opening-a-file)。

## <a name="read-requests"></a>读取请求


若要检索的读取请求的缓冲区 ([**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read))，WDF 驱动程序调用其中一种**WdfRequestRetrieveOutputXxx**方法。 这些方法返回的每个依赖于是否缓冲区驱动程序执行[缓冲，直接或都不 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)。

缓冲区指针的 WDM 等效项有关的信息，请参阅[KMDF 缓冲区指针的 WDM 等效](wdm-equivalents-for-kmdf-buffer-pointers.md#read)。

## <a name="write-requests"></a>写入请求


若要检索的写入请求的缓冲区 ([**IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write))，WDF 驱动程序调用其中一种**WdfRequestRetrieveInputXxx**方法。 这些方法返回的每个依赖于是否缓冲区驱动程序执行[缓冲，直接或都不 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)。

缓冲区指针的 WDM 等效项有关的信息，请参阅[KMDF 缓冲区指针的 WDM 等效](wdm-equivalents-for-kmdf-buffer-pointers.md#write)。

## <a name="device-io-control-requests"></a>设备 I/O 控制请求


若要处理设备 I/O 控制请求 ([**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control))，WDF 驱动程序拨打**WdfRequestRetrieveInputXxx**方法或**WdfRequestRetrieveOutputXxx**用于获得缓冲区相对于缓冲和直接 I/O 的方法。 相应的输入和输出方法返回同一缓冲区，因此驱动程序可以使用其中任何一个。 这些方法返回的每个依赖于是否缓冲区驱动程序执行[缓冲，直接或都不 I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)，只需为在读取和写入请求。

如果该驱动程序处理源自另一个设备堆栈或使用的设备 I/O 控制请求**Parameters.Other**字段，该驱动程序应调用[ **WdfRequestGetParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)若要获取的缓冲区指针而不是调用[ **WdfRequestRetrieveInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)并[ **WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer). 因为这些请求的源保证是内核模式组件，该驱动程序可以信任返回的缓冲区指针。 但是，它仍然必须验证的缓冲区长度和任何其他参数。

缓冲区指针的 WDM 等效项有关的信息，请参阅[KMDF 缓冲区指针的 WDM 等效](wdm-equivalents-for-kmdf-buffer-pointers.md#device-control)。

## <a name="internal-device-io-control-requests"></a>内部设备 I/O 控制请求


内部设备 I/O 控制请求 ([**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)) 只能由内核模式组件颁发，并且某些操作系统组件在内部用来传递请求块 (如 SCSI xRB 协议请求块\[Srb\]或通用请求块\[URBs\])。 许多不同类型的缓冲区可以附带此类请求。

检索并解释内部设备 I/O 控制请求的参数可能存在问题。 出现问题，因为某些此类请求将传递在长度**InputBufferLength**并**OutputBufferLength**的字段**Parameters.DeviceIoControl**结构的 WDM IRP，但一些不适用。 不过，框架会提取中的任何有效值**InputBufferLength**并**OutputBufferLength**字段并将它们作为参数传递[ *EvtIoInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)回调。 它不执行任何内部验证这些值。

若要获取缓冲区本身，该驱动程序调用以下方法之一：

-   [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)，它将返回**Parameters.DeviceIoControl.Type3InputBuffer** IRP 的字段。
-   [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)，它将返回**UserBuffer** IRP 的字段。

 

 





