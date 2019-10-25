---
title: 将 I/O 调度例程移植到 I/O 事件回调函数
description: 将 I/O 调度例程移植到 I/O 事件回调函数
ms.assetid: 0BD65185-C358-4E28-8E31-255AF8D77F93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e338a030a167b9dcc89cb41806fb909392bf9774
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845210"
---
# <a name="porting-io-dispatch-routines-to-io-event-callback-functions"></a>将 I/O 调度例程移植到 I/O 事件回调函数


WDM 驱动程序的 i/o 调度例程的核心映射到 WDF 驱动程序的 i/o 事件回调函数。 但是，i/o 事件回调函数的不同之处在于 WDM 驱动程序的 i/o 调度例程：

-   当框架调用 WDF 驱动程序的 i/o 事件回调时，回调会接收处于 noncancelable 状态的请求。 除非驱动程序将该请求明确标记为可取消，否则无法取消该请求。
-   驱动程序指定框架是否同步对 i/o 事件回调的调用，以便仅对每个队列或每个设备对象同时运行一个此类回调，或者框架是否根本不应用同步。 有关选择同步选项的详细信息，请参阅[使用自动同步](using-automatic-synchronization.md)。

这些差异意味着大多数 i/o 事件回调函数包含的代码明显小于同步访问的代码，并可防止争用条件与相应的 WDM **DispatchXxx**例程相比较。

除了同步以外，WDM 驱动程序的 i/o 调度例程与 WDF 驱动程序的 i/o 事件回调函数之间的主要区别在于驱动程序如何检索参数以及如何访问 i/o 缓冲区。

## <a name="parameters-for-io-requests"></a>I/o 请求的参数


根据 WDF 驱动程序处理的请求类型及其 i/o 队列的配置方式，可能无需驱动程序将参数作为 WDM 驱动程序来分析为 i/o 请求。 当框架为读取、写入和设备 i/o 控制请求（[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)、 [*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)、 [*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)、 [*EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)）调用 i/o 事件回调时，它将提取最常使用的IRP 中的参数，并将其作为参数传递给回调。 例如，框架使用 WDFREQUEST 对象的句柄和要读取的字节数调用驱动程序的*EvtIoRead*回调。 如果驱动程序无需设备偏移量或排序键，则可以通过调用**WdfRequestRetrieveOutputXxx**方法之一，只需从 WDFREQUEST 对象检索缓冲区;它不需要检索其他参数。

但是，在**EvtIoDefault**回调中，框架只将句柄传递给队列，将句柄传递给 request 对象。 因此，驱动程序必须调用**WdfRequestGetParameters**以获取参数，包括请求类型（**WdfRequestTypeXxx**）。 [**WdfRequestGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)返回一个[**WDF\_请求\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_parameters)结构，其中包含与创建、读取、写入、设备 i/o 控制或内部设备 i/o 控制请求一起传递的参数。

## <a name="access-to-buffers-for-buffered-and-direct-io"></a>用于缓冲和直接 i/o 的缓冲区访问


当框架收到 i/o 请求时，它将创建一个 WDFREQUEST 对象，该对象封装基础 WDM IRP。 然后，它会将 WDFREQUEST 对象排队，并最终按照队列的驱动程序[调度规范](dispatching-methods-for-i-o-requests.md)调度该对象。 驱动程序使用 WDF 方法检索 i/o 请求的参数和缓冲区。 驱动程序可以通过调用[**WdfRequestWdmGetIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)随时获取基础 WDM IRP。

与 WDM 驱动程序一样，WDF 驱动程序可以支持[缓冲、直接或非](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)i/o。 驱动程序在创建设备对象之前，通过在[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调中调用[**WdfDeviceInitSetIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)来设置每个设备对象支持的 i/o 类型。 然而，与 WDM 驱动程序不同的是，KMDF 驱动程序以相同的方式访问缓冲区，无论是执行缓冲还是直接 i/o，并为每个缓冲区使用相同的方法。

尽管 WDF 驱动程序以相同的方式访问缓冲和直接 i/o 的缓冲区，但它使用不同的方法来检索缓冲区，具体取决于 i/o 请求的类型。 以下各节介绍了驱动程序如何处理每种类型的 i/o 请求：

-   [创建请求](#create-requests)
-   [读取请求](#read-requests)
-   [写入请求](#write-requests)
-   [设备 i/o 控制请求](#device-io-control-requests)
-   [内部设备 i/o 控制请求](#internal-device-io-control-requests)

## <a name="create-requests"></a>创建请求


WDF 驱动程序可以通过以下两种方式之一处理创建请求（[**IRP\_MJ\_create**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)）：

-   绕过队列，并提供[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调。
-   让框架队列创建请求并实现[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)回调，以处理来自队列的此类请求。

有关处理文件创建请求的详细信息，请参阅[框架文件对象](framework-file-objects.md#creating-or-opening-a-file)。

## <a name="read-requests"></a>读取请求


若要检索读取请求的缓冲区（[**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)），WDF 驱动程序将调用**WdfRequestRetrieveOutputXxx**方法之一。 其中每个方法返回的缓冲区取决于驱动程序执行的是[缓冲、直接还是非](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)i/o。

有关缓冲区指针的 WDM 等效项的信息，请参阅[KMDF 缓冲区指针的 Wdm 等效](wdm-equivalents-for-kmdf-buffer-pointers.md#read)项。

## <a name="write-requests"></a>写入请求


若要检索写入请求的缓冲区（[**IRP\_MJ\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)），WDF 驱动程序将调用**WdfRequestRetrieveInputXxx**方法之一。 其中每个方法返回的缓冲区取决于驱动程序执行的是[缓冲、直接还是非](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)i/o。

有关缓冲区指针的 WDM 等效项的信息，请参阅[KMDF 缓冲区指针的 Wdm 等效](wdm-equivalents-for-kmdf-buffer-pointers.md#write)项。

## <a name="device-io-control-requests"></a>设备 i/o 控制请求


为了处理设备 i/o 控制请求（[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)），WDF 驱动程序调用**WdfRequestRetrieveInputXxx**方法或**WdfRequestRetrieveOutputXxx**方法来获取缓冲的缓冲区和直接 i/o。 对应的输入和输出方法返回同一个缓冲区，因此驱动程序可以使用其中的一个。 其中每个方法返回的缓冲区取决于驱动程序执行的是[缓冲、直接或非](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)i/o，就像在读取和写入请求中一样。

如果驱动程序处理来自其他设备堆栈的设备 i/o 控制请求或使用**参数。其他**字段，驱动程序应调用[**WdfRequestGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)来获取缓冲区指针，而不是调用[**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)和[**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)。 由于这些请求的源保证是内核模式组件，因此驱动程序可以信任返回的缓冲区指针。 但是，它仍必须验证缓冲区长度和任何其他参数。

有关缓冲区指针的 WDM 等效项的信息，请参阅[KMDF 缓冲区指针的 Wdm 等效](wdm-equivalents-for-kmdf-buffer-pointers.md#device-control)项。

## <a name="internal-device-io-control-requests"></a>内部设备 i/o 控制请求


内部设备 i/o 控制请求（[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)）仅由内核模式组件颁发，由某些操作系统组件在内部使用，用于传递请求块（bet-hx-xrb 协议例如，SCSI 请求块 \[SRBs\] 或通用请求块 \[URBs\]）。 许多不同类型的缓冲区可能伴随此类请求。

检索和解释内部设备 i/o 控制请求的参数可能会有问题。 之所以出现此问题，是因为某些此类请求会传递**DeviceIoControl**结构的**InputBufferLength**和**OutputBufferLength**字段中的长度，但有些则不会。 尽管如此，框架提取**InputBufferLength**和**OutputBufferLength**字段中的任何值，并将它们作为参数传递给[*EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)回调。 它不对这些值执行任何内部验证。

若要自行获取缓冲区，驱动程序将调用以下方法之一：

-   [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)，它返回 IRP 的**DeviceIoControl. Type3InputBuffer**字段。
-   [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)，它返回 IRP 的**UserBuffer**字段。

 

 





