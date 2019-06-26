---
title: 使用驱动程序定义的接口
description: 使用驱动程序定义的接口
ms.assetid: ad96add6-c982-429b-b815-d7adf6fed8cc
keywords:
- 驱动程序定义的接口 WDK KMDF
- WDK KMDF 接口
- 单向通信 WDK KMDF
- WDK KMDF 的双向通信
- 引用计数 WDK KMDF
- 引用函数 WDK KMDF
- 取消引用函数 WDK KMDF
- 不执行任何操作函数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57fafacf2bc9c7f782392f294a11923d25396f05
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372263"
---
# <a name="using-driver-defined-interfaces"></a>使用驱动程序定义的接口


驱动程序可以定义其他驱动程序可以访问的特定于设备的接口。 这些*驱动程序定义的接口*可包含的一组可调用的例程、 一组数据结构，或两者。 该驱动程序通常会提供指向这些例程和驱动程序定义的接口结构，该驱动程序使其可供其他驱动程序中的结构的指针。

例如，总线驱动程序可能会提供更高级别的驱动程序可以调用来获取信息的子设备，如果该信息不可用子设备的资源列表中的一个或多个例程。

有关驱动程序定义的接口在 WDK 中所述的一组的示例，请参阅[USB 例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85))。 此外，请参阅基于 framework 的版本[toaster](sample-kmdf-drivers.md)示例。

### <a name="creating-an-interface"></a>创建一个接口

指定每个驱动程序定义的接口：

-   一个 GUID

-   版本号

-   驱动程序定义的接口结构

-   引用，并取消引用例程

若要创建一个接口，并使其可供其他驱动程序，基于框架的驱动程序可以使用以下步骤：

1.  定义接口结构。

    此驱动程序定义的结构的第一个成员必须是[**界面**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)标头结构。 其他成员可能包含接口的数据和指针的另一种驱动程序可以调用到其他结构或例程。

    您的驱动程序必须提供[ **WDF\_查询\_接口\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/ns-wdfqueryinterface-_wdf_query_interface_config)结构，其中描述了已定义的接口。

2.  调用[ **WdfDeviceAddQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)。

    [ **WdfDeviceAddQueryInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)方法执行以下操作：

    -   存储接口，如其 GUID、 版本号和结构大小的信息，因此框架可以识别的接口的另一个驱动程序的请求。
    -   注册一个可选[ *EvtDeviceProcessQueryInterfaceRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)事件回调函数，框架将调用另一个驱动程序要求接口时。

驱动程序定义的接口的每个实例都与单个设备，关联，因此驱动程序通常调用[ **WdfDeviceAddQueryInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)中[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)或[ *EvtChildListCreateDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)回调函数。

### <a name="accessing-an-interface"></a>访问接口

如果您的驱动程序已定义了一个接口，另一个基于 framework 的驱动程序可以通过调用请求对接口的访问[ **WdfFdoQueryForInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoqueryforinterface)并传递 GUID、 版本号、 指向结构和结构大小。 框架创建的 I/O 请求，并将其发送到驱动程序堆栈的顶部。

驱动程序通常会调用[ **WdfFdoQueryForInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoqueryforinterface)中[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 或者，如果设备不处于工作状态时，该驱动程序必须释放该接口，该驱动程序可以调用**WdfFdoQueryForInterface**内[ *EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数并调用该接口的取消引用中的例程[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数。

如果驱动程序的要求提供驱动程序 B 接口 B 已定义该驱动程序，该框架将处理的请求驱动程序 b。框架验证，GUID 和版本表示受支持的界面，并且结构大小该驱动程序提供足够大以保存该接口。

当驱动程序调用[ **WdfFdoQueryForInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoqueryforinterface)，则框架将创建 I/O 请求传输到驱动程序堆栈的底部。 如果一个简单的驱动程序堆栈包含-A、 B 和 C 的三个驱动程序和驱动程序的要求提供一个接口，则驱动程序 B 和 C 的驱动程序可以支持的接口。 例如，驱动程序 B 之前将传递到驱动程序 C.驱动程序 C 请求可提供可能会填在驱动程序 A 的接口结构[ *EvtDeviceProcessQueryInterfaceRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)回调函数检查接口结构的内容，并可能修改它们。

如果驱动程序的所需访问驱动程序 B 的接口和驱动程序 B 是远程的 I/O 目标 （即，驱动程序中不同的驱动程序堆栈），一个驱动程序必须调用[ **WdfIoTargetQueryForInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetqueryforinterface)而不是[ **WdfFdoQueryForInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoqueryforinterface)。

### <a name="using-one-way-or-two-way-communication"></a>使用单向或双向通信

可以定义一个接口，提供单向通信，或其中一个提供双向通信。 若要指定驱动程序集的双向通信**ImportInterface**的成员及其[ **WDF\_查询\_接口\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/ns-wdfqueryinterface-_wdf_query_interface_config)结构**TRUE**。

如果该接口提供单向通信，并且驱动程序的要求提供驱动程序 B 的接口，接口的数据流仅从驱动程序 B 到驱动程序 a。当框架收到支持单向通信的接口的驱动程序 A 的请求时，该框架将驱动程序定义的接口值复制到驱动程序 A 的接口结构。 然后，它调用驱动程序 B [ *EvtDeviceProcessQueryInterfaceRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)回调函数，如果存在，因此它可以检查和修改接口值。

如果该接口提供双向通信，接口结构包含一些成员填写发送对驱动程序 B.驱动程序 B 的请求可以读取的参数值的该驱动程序之前提供，做出选择，有关基于对这些值，该驱动程序要提供给 A.驱动程序的信息框架收到支持双向通信的接口的驱动程序 A 的请求后，框架将调用驱动程序 B [ *EvtDeviceProcessQueryInterfaceRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)回调函数，它可以检查接收值并提供输出值。 对于双向通信，回调函数是必需的这是因为框架不会复制到驱动程序 A 的接口结构的接口的任何值。

### <a name="maintaining-a-reference-count"></a>维护引用计数

每个接口必须包含引用函数和取消引用函数，其递增和递减引用计数的接口。 定义的接口的驱动程序指定的地址中的这些函数及其[**界面**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)结构。

当驱动程序的驱动程序 B 要求提供一个接口时，框架将使该接口可用于驱动程序 A.之前调用接口的引用函数当驱动程序的已完成使用界面时，它必须调用接口的取消引用函数。

引用和大多数接口可以是不执行任何操作函数不执行任何操作的取消引用的函数。 该框架提供了执行任何操作引用计数函数[ **WdfDeviceInterfaceReferenceNoOp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceinterfacereferencenoop)并[ **WdfDeviceInterfaceDereferenceNoOp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceinterfacedereferencenoop)，可供大多数驱动程序。

驱动程序必须保持的唯一时间跟踪的接口的引用计数，并提供实际引用和取消引用函数，是从远程 I/O 目标 （即，驱动程序中不同的驱动程序堆栈） 驱动程序的请求的接口时。 在这种情况下，驱动程序 B （在不同的堆栈） 必须实现引用计数，以便它可防止其设备驱动程序的使用驱动程序 B 的接口的删除。

如果您正在设计驱动程序 B，后者定义一个接口，您必须决定是否将从不同的驱动程序堆栈中访问您的驱动程序接口。 （B 的驱动程序无法确定其接口的请求是否从本地驱动程序堆栈中或从远程堆栈。）如果您的驱动程序将支持来自远程堆栈接口请求，该驱动程序必须实现引用计数。

如果您正在设计驱动程序 A，访问远程 I/O 目标上的接口，该驱动程序必须提供[ *EvtIoTargetQueryRemove* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)释放接口的回调函数时驱动程序 B 的设备是将要移除[ *EvtIoTargetRemoveComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)当驱动程序 B 的设备是意外删除，释放接口的回调函数[ *EvtIoTargetRemoveCanceled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)重新获取该接口，如果尝试删除该设备已被取消的回调函数。

 

 





