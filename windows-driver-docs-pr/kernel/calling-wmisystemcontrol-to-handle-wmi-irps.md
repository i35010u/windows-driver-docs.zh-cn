---
title: 调用 WmiSystemControl 以处理 WMI IRP
description: 调用 WmiSystemControl 以处理 WMI IRP
keywords:
- WMI WDK 内核，请求
- 请求 WDK WMI
- Irp WDK WMI
- WmiSystemControl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cea1c454392bfd5d144259c28de3db50b3d9175
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091078"
---
# <a name="calling-wmisystemcontrol-to-handle-wmi-irps"></a>调用 WmiSystemControl 以处理 WMI IRP





WMI 库例程简化了 WMI 请求的处理，因为无需处理每个此类请求，驱动程序将调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)。 在 **WmiSystemControl** 调用中，驱动程序将包含指向驱动程序的 [WMI 库回调例程](/windows-hardware/drivers/ddi/wmilib)的入口点的已初始化 [**WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)结构传递 (*DpWmiXxx* 例程) 以及有关驱动程序的数据块和事件块的信息。

由于 WMI 库不提供用于传递动态实例名称或静态实例名称列表的机制，因此驱动程序可以使用 WMI 库来处理仅涉及静态实例名称的数据块的请求（基于 PDO 或单个基名称字符串）。 有关静态和动态实例名称的详细信息，请参阅 [定义 WMI 实例名称](defining-wmi-instance-names.md)。 任何内容都不会阻止驱动程序使用 WMI 库处理此类块的请求，并处理其 [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中其他块的请求。 有关详细信息，请参阅 [在 DispatchSystemControl 例程中处理 WMI irp](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)。

若要通过调用 **WmiSystemControl** 来处理 WMI irp，驱动程序必须实现某些必需的 *DpWmiXxx* 回调例程，并可能实现其他可选的 *DpWmiXxx* 回调例程：

-   [*DpWmiQueryReginfo*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)- (必需的) 提供有关驱动程序所注册的数据和事件块的信息。 WMI 调用驱动程序的 *DpWmiQueryReginfo* 例程来处理 [**IRP \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 或 [**irp \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) 请求。 有关详细信息，请参阅 [使用 WMI 库注册块](using-the-wmi-library-to-register-blocks.md)。

-   [*DpWmiQueryDataBlock*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)- (必需的) 返回数据块的单个实例或所有实例。 WMI 调用驱动程序的 *DpWmiQueryDataBlock* 例程来处理 [**IRP \_ MN \_ 查询 \_ 单一 \_ 实例**](./irp-mn-query-single-instance.md) 或 [**irp \_ MN \_ 查询 \_ 所有 \_ 数据**](./irp-mn-query-all-data.md) 请求。

-   [*DpWmiSetDataBlock*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)- (可选) 更改数据块的单个实例中的所有数据项。 WMI 调用驱动程序的 *DpWmiSetDataBlock* 例程来处理 [**IRP \_ MN \_ CHANGE \_ 单一 \_ 实例**](./irp-mn-change-single-instance.md) 请求。

-   [*DpWmiSetDataItem*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)- (可选) 更改数据块实例中的单个数据项。 WMI 调用驱动程序的 *DpWmiSetDataItem* 例程来处理 [**IRP \_ MN \_ CHANGE \_ 单项 \_**](./irp-mn-change-single-item.md) 请求。

-   [*DpWmiFunctionControl*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)- (可选) 启用和禁用注册开销较高的块的事件通知和数据收集。 WMI 调用驱动程序的 *DpWmiFunctionControl* 例程来处理 [**IRP \_ MN \_ 启用 \_ 收集**](./irp-mn-enable-collection.md)、 [**irp \_ MN \_ 禁用 \_ 收集**](./irp-mn-disable-collection.md)、 [**irp \_ MN \_ 启用 \_ 事件**](./irp-mn-enable-events.md)或 [**irp \_ MN \_ DISABLE \_ events**](./irp-mn-disable-events.md) 请求。

-   [*DpWmiExecuteMethod*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)- (可选) 执行与数据块关联的方法。 WMI 调用驱动程序的 *DpWmiExecuteMethod* 例程来处理 [**IRP \_ MN \_ EXECUTE \_ 方法**](./irp-mn-execute-method.md) 请求。

驱动程序的 *DpWmiXxx* 例程可以具有驱动程序编写器选择的任何名称。

在调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)之前，驱动程序必须使用入口点将 [**WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context) 结构初始化为其 *DpWmiXxx* 例程，并提供有关其数据块和事件块的信息。

当驱动程序收到 WMI 请求时：

1. 驱动程序调用 **WmiSystemControl** ，该指针指向其初始化的 **WMILIB \_ 上下文** 结构、指向其设备对象的指针和指向 IRP 的指针。

2. WMI 将验证 IRP 参数，并调用驱动程序的 *DpWmiXxx* 例程来处理请求。 如果驱动程序在其 **WMILIB \_ 上下文** 中设置了可选 *DpWmiXxx* 例程的入口点，WMI 将使用默认值和状态完成 IRP。

3. 在其 *DpWmiXxx* 例程中，驱动程序处理请求并将任何输出写入调用方提供的缓冲区。 例如，驱动程序的 [*DpWmiQueryDataBlock*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback) 例程会将指定块) 请求的 (实例写入缓冲区。

4. 对于除 [*DpWmiQueryReginfo*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)以外的所有 *DpWmiXxx* 例程，驱动程序将调用 [**WmiCompleteRequest**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmicompleterequest)来完成请求，或返回挂起完成的状态 \_ （对于任何 IRP）。

5. WMI 执行任何必要的后处理，将任何输出打包为适当的 **WNODE \_ * XXX*** 结构，并将输出和状态传递到数据使用者。

 

