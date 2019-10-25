---
title: 调用 WmiSystemControl 以处理 WMI IRP
description: 调用 WmiSystemControl 以处理 WMI IRP
ms.assetid: a2fa53e2-6468-4c3c-8b41-9a97305abc43
keywords:
- WMI WDK 内核，请求
- 请求 WDK WMI
- Irp WDK WMI
- WmiSystemControl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a67216bde594957962bea380bbe2863ff35f727a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828571"
---
# <a name="calling-wmisystemcontrol-to-handle-wmi-irps"></a>调用 WmiSystemControl 以处理 WMI IRP





WMI 库例程简化了 WMI 请求的处理，因为无需处理每个此类请求，驱动程序将调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)。 在**WmiSystemControl**调用中，驱动程序将一个已初始化的[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)结构，其中包含驱动程序的[WMI 库回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)（*DpWmiXxx*例程）的入口点和有关驱动程序的数据块和事件块。

由于 WMI 库不提供用于传递动态实例名称或静态实例名称列表的机制，因此驱动程序可以使用 WMI 库来处理仅涉及静态实例名称的数据块的请求（基于 PDO 或单个基名称字符串）。 有关静态和动态实例名称的详细信息，请参阅[定义 WMI 实例名称](defining-wmi-instance-names.md)。 任何内容都不会阻止驱动程序使用 WMI 库处理此类块的请求，并处理其[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中其他块的请求。 有关详细信息，请参阅[在 DispatchSystemControl 例程中处理 WMI irp](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)。

若要通过调用**WmiSystemControl**来处理 WMI irp，驱动程序必须实现某些必需的*DpWmiXxx*回调例程，并可能实现其他可选的*DpWmiXxx*回调例程：

-   [*DpWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)-（必需）提供有关驱动程序正在注册的数据和事件块的信息。 WMI 调用驱动程序的*DpWmiQueryReginfo*例程来处理[**IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)或[**irp\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)请求。 有关详细信息，请参阅[使用 WMI 库注册块](using-the-wmi-library-to-register-blocks.md)。

-   [*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)-（必需）返回数据块的单个实例或所有实例。 WMI 调用驱动程序的*DpWmiQueryDataBlock*例程来处理[**IRP\_MN\_query\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)或 IRP\_\_\_\_[**所有数据**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)请求。

-   [*DpWmiSetDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)-（可选）更改数据块的单个实例中的所有数据项。 WMI 调用驱动程序的*DpWmiSetDataBlock*例程来处理[**IRP\_MN\_更改\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)请求。

-   [*DpWmiSetDataItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)-（可选）更改数据块的实例中的单个数据项。 WMI 调用驱动程序的*DpWmiSetDataItem*例程来处理[**IRP\_MN\_更改\_单一\_项**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)请求。

-   [*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)-（可选）启用和禁用注册开销较高的块的事件通知和数据收集。 WMI 调用驱动程序的*DpWmiFunctionControl*例程来处理[**IRP\_MN\_启用\_收集**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)、 [**irp\_MN\_禁用\_收集**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)、 [**irp\_MN\_启用\_EVENTS**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)或[**IRP\_MN\_禁用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)请求。

-   [*DpWmiExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)-（可选）执行与数据块关联的方法。 WMI 调用驱动程序的*DpWmiExecuteMethod*例程来处理[**IRP\_MN\_执行\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)请求。

驱动程序的*DpWmiXxx*例程可以具有驱动程序编写器选择的任何名称。

在调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)之前，驱动程序必须使用*DpWmiXxx*例程的入口点和有关其数据块和事件块的信息来初始化[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)结构。

当驱动程序收到 WMI 请求时：

1. 驱动程序调用**WmiSystemControl** ，该指针指向其已初始化的**WMILIB\_上下文**结构、指向其设备对象的指针和指向 IRP 的指针。

2. WMI 将验证 IRP 参数，并调用驱动程序的*DpWmiXxx*例程来处理请求。 如果驱动程序在其 **\_WMILIB**中没有设置入口点，则对于可选*DPWMIXXX*例程，WMI 将使用默认值和状态完成 IRP。

3. 在其*DpWmiXxx*例程中，驱动程序处理请求并将任何输出写入调用方提供的缓冲区。 例如，驱动程序的[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程会将指定的块的请求实例写入缓冲区。

4. 对于除[*DpWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)以外的所有*DpWmiXxx*例程，驱动程序将调用[**WmiCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmicompleterequest)来完成请求，或返回状态\_"挂起" 以推迟完成，与任何 IRP 相同。

5. WMI 执行任何必要的后处理，将任何输出打包为适当的**WNODE\_* XXX*** 结构，并将输出和状态传递到数据使用者。

 

 




