---
title: 使用驱动程序定义的接口
description: 使用驱动程序定义的接口
ms.assetid: ad96add6-c982-429b-b815-d7adf6fed8cc
keywords:
- 驱动程序定义的接口 WDK KMDF
- 接口 WDK KMDF
- 单向通信 WDK KMDF
- 双向通信 WDK KMDF
- 引用计数 WDK KMDF
- 引用函数 WDK KMDF
- 取消引用函数 WDK KMDF
- 无 op 函数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40228dff9f6e1d2483cb4a6b1549875fa2e96895
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184541"
---
# <a name="using-driver-defined-interfaces"></a>使用驱动程序定义的接口


驱动程序可以定义其他驱动程序可以访问的特定于设备的接口。 这些 *驱动程序定义的接口* 可以包含一组可调用例程、一组数据结构或两者。 驱动程序通常在驱动程序定义的接口结构中提供指向这些例程和结构的指针，驱动程序可供其他驱动程序使用。

例如，如果子设备的资源列表中没有此信息，则总线驱动程序可能会提供一个或多个例程，更高级别的驱动程序可以调用此例程来获取有关子设备的信息。

有关在 WDK 中记录的一组驱动程序定义的接口的示例，请参阅 [USB 例程](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85))。 另请参阅 [toaster](sample-kmdf-drivers.md) 示例的基于框架的版本。

### <a name="creating-an-interface"></a>创建接口

每个驱动程序定义的接口都由以下各项指定：

-   GUID

-   版本号

-   驱动程序定义的接口结构

-   引用和取消引用例程

若要创建接口并使其可供其他驱动程序使用，基于框架的驱动程序可以使用以下步骤：

1.  定义接口结构。

    此驱动程序定义的结构的第一个成员必须是 [**接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface) 标头结构。 其他成员可能包括接口数据以及另一个台驱动程序可调用的其他结构或例程的指针。

    你的驱动程序必须提供一个 [**WDF \_ 查询 \_ 接口 \_ 配置**](/windows-hardware/drivers/ddi/wdfqueryinterface/ns-wdfqueryinterface-_wdf_query_interface_config) 结构，该结构描述你定义的接口。

2.  调用 [**WdfDeviceAddQueryInterface**](/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)。

    [**WdfDeviceAddQueryInterface**](/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface)方法执行以下操作：

    -   存储有关接口的信息，如其 GUID、版本号和结构大小，以便框架可以识别其他驱动程序的接口请求。
    -   注册一个可选的 [*EvtDeviceProcessQueryInterfaceRequest*](/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request) 事件回调函数，当另一个驱动程序请求该函数时，框架将调用该函数。

驱动程序定义接口的每个实例都与单个设备相关联，因此，驱动程序通常从[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)或[*EvtChildListCreateDevice*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)回调函数中调用[**WdfDeviceAddQueryInterface**](/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceaddqueryinterface) 。

### <a name="accessing-an-interface"></a>访问接口

如果驱动程序定义了接口，则另一个基于框架的驱动程序可以通过调用 [**WdfFdoQueryForInterface**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoqueryforinterface) 并传递 GUID、版本号、指向结构的指针和结构大小来请求对接口的访问。 框架创建 i/o 请求并将其发送到驱动程序堆栈的顶部。

驱动程序通常从[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数中调用[**WdfFdoQueryForInterface**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoqueryforinterface) 。 或者，如果驱动程序必须在设备处于工作状态时释放接口，则驱动程序可以从[*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数中调用**WdfFdoQueryForInterface** ，并从[*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数内调用接口的取消引用例程。

如果驱动程序 A 为驱动程序 B 定义的接口请求驱动程序 b，则框架将处理驱动程序 B 的请求。该框架验证 GUID 和版本是否表示支持的接口，以及驱动程序 A 提供的结构大小是否足以容纳该接口。

当驱动程序调用 [**WdfFdoQueryForInterface**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoqueryforinterface)时，框架创建的 i/o 请求将一直传播到驱动程序堆栈的底部。 如果简单驱动程序堆栈包含三个驱动程序： A、B 和 C，并且如果驱动程序 A 要求提供接口，则驱动程序 B 和驱动程序 C 都可以支持接口。 例如，在将请求传递给驱动程序 C 之前，驱动程序 B 可能会填充驱动程序 A 的接口结构。驱动程序 C 可以提供一个 [*EvtDeviceProcessQueryInterfaceRequest*](/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request) 回调函数，用于检查接口结构的内容，并可能修改这些内容。

如果驱动程序 A 需要访问驱动程序 B 的接口，并且驱动程序 B 是远程 i/o 目标 (也就是说，位于不同驱动程序堆栈) 中的驱动程序必须调用 [**WdfIoTargetQueryForInterface**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetqueryforinterface) 而不是 [**WdfFdoQueryForInterface**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoqueryforinterface)。

### <a name="using-one-way-or-two-way-communication"></a>使用单向或双向通信

你可以定义提供单向通信的接口，也可以定义一个提供双向通信的接口。 若要指定双向通信，驱动程序会将其[**WDF \_ 查询 \_ 接口 \_ 配置**](/windows-hardware/drivers/ddi/wdfqueryinterface/ns-wdfqueryinterface-_wdf_query_interface_config)结构的**ImportInterface**成员设置为**TRUE**。

如果接口提供单向通信，并且驱动程序 A 请求驱动程序 B 的接口，则接口数据仅流向驱动程序 B 的驱动程序 A。当框架收到驱动程序 A 对支持单向通信的接口的请求时，框架会将驱动程序定义的接口值复制到驱动程序 A 的接口结构。 然后，它调用驱动程序 B 的 [*EvtDeviceProcessQueryInterfaceRequest*](/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request) 回调函数（如果存在），以便它可以检查并可能修改接口值。

如果接口提供双向通信，则在将请求发送到驱动程序 B 之前，接口结构将包含驱动程序 A 填充的一些成员。驱动程序 B 可以读取驱动程序提供的参数值，并根据这些值进行选择，以了解向驱动程序 A 提供哪些信息。当框架收到驱动程序 A 对支持双向通信的接口的请求时，框架将调用驱动程序 B 的 [*EvtDeviceProcessQueryInterfaceRequest*](/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request) 回调函数，以便它可以检查接收的值并提供输出值。 对于双向通信，回调函数是必需的，因为框架不会将任何接口值复制到驱动程序 A 的接口结构。

### <a name="maintaining-a-reference-count"></a>维护引用计数

每个接口都必须包含一个引用函数和一个取消引用函数，该函数递增和递减接口的引用计数。 定义接口的驱动程序在其 [**接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface) 结构中指定这些函数的地址。

当驱动程序 A 向驱动程序请求接口 B 时，框架会在使接口可供驱动程序使用之前调用接口的 reference 函数。当驱动程序 A 完成使用接口时，它必须调用接口的取消引用函数。

大多数接口的引用和取消引用函数可以是不执行任何操作的无操作函数。 该框架提供了大多数驱动程序可以使用的无操作引用计数函数（ [**WdfDeviceInterfaceReferenceNoOp**](/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceinterfacereferencenoop) 和 [**WdfDeviceInterfaceDereferenceNoOp**](/windows-hardware/drivers/ddi/wdfqueryinterface/nf-wdfqueryinterface-wdfdeviceinterfacedereferencenoop)）。

只有当驱动程序 A 从远程 i/o 目标请求接口时，驱动程序才必须跟踪接口的引用计数，并提供实际引用和取消引用函数，这是因为驱动程序 A 从远程 i/o 目标请求接口 (即，位于不同驱动程序堆栈中的驱动程序) 。 在这种情况下，驱动程序 B (在不同的堆栈中) 必须实现引用计数，以便当驱动程序 A 使用驱动程序 B 的接口时，它可以阻止删除其设备。

如果设计的驱动程序 B 定义了接口，则必须决定是否从其他驱动程序堆栈访问驱动程序的接口。  (驱动程序 B 无法确定其接口的请求是来自本地驱动程序堆栈还是来自远程堆栈的请求 ) 。如果您的驱动程序将支持来自远程堆栈的接口请求，则驱动程序必须实现引用计数。

如果正在设计驱动程序 A，在远程 i/o 目标上访问接口时，驱动程序必须提供一个[*EvtIoTargetQueryRemove*](/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)回调函数，该函数可在要删除驱动程序 b 的设备时释放接口，EvtIoTargetRemoveComplete 回调函数（当驱动程序 b 的设备被意外删除时，释放接口的[*EvtIoTargetRemoveComplete*](/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)回调函数）和一个[*EvtIoTargetRemoveCanceled*](/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)回调函数（如果删除该设备的尝试被取消）。

 

