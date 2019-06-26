---
title: 调用 WmiSystemControl 以处理 WMI IRP
description: 调用 WmiSystemControl 以处理 WMI IRP
ms.assetid: a2fa53e2-6468-4c3c-8b41-9a97305abc43
keywords:
- WMI WDK 内核请求
- 请求 WDK WMI
- Irp WDK WMI
- WmiSystemControl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3af17b88cf9e58ae2d7ea38a15da9d6fc6ca0b2b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387015"
---
# <a name="calling-wmisystemcontrol-to-handle-wmi-irps"></a>调用 WmiSystemControl 以处理 WMI IRP





WMI 库例程简化处理的 WMI 请求，因为驱动程序而不是处理每个此类请求，调用[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)。 在中**WmiSystemControl**调用时，驱动程序通过一个初始化[ **WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)到驱动程序的结构，其中包含入口点[WMI 库回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)(*DpWmiXxx*例程) 以及有关驱动程序的数据块和事件块的信息。

由于 WMI 库提供传递动态实例名称或静态实例名称列表的机制，因此驱动程序可以使用 WMI 库来处理包含具有基于 PDO 或单个基名称字符串的静态实例名称的唯一数据块的请求。 有关静态和动态实例名称的详细信息，请参阅[定义 WMI 实例名](defining-wmi-instance-names.md)。 没有任何障碍的驱动程序由 WMI 库用于处理此类块的请求和处理请求，针对中的其他块，其[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 有关详细信息，请参阅[DispatchSystemControl 例程中处理 WMI Irp](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)。

若要通过调用处理 WMI Irp **WmiSystemControl**，驱动程序必须实现某些所需*DpWmiXxx*回调例程，可能实现其他可选*DpWmiXxx*回调例程：

-   [*DpWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)—(Required) 提供有关数据和事件的信息会阻止正在注册驱动程序。 WMI 调用驾*DpWmiQueryReginfo*到进程例程[ **IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)或[ **IRP\_MN\_REGINFO\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)请求。 有关详细信息，请参阅[使用 WMI 库对注册块](using-the-wmi-library-to-register-blocks.md)。

-   [*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)—(Required) 返回单一实例或数据块的所有实例。 WMI 调用驾*DpWmiQueryDataBlock*到进程例程[ **IRP\_MN\_查询\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)或[ **IRP\_MN\_查询\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)请求。

-   [*DpWmiSetDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_datablock_callback)—(Optional) 更改的数据块的单个实例中的所有数据项。 WMI 调用驾*DpWmiSetDataBlock*到进程例程[ **IRP\_MN\_更改\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)请求。

-   [*DpWmiSetDataItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_dataitem_callback)—(Optional) 更改一个数据块的实例中的数据项。 WMI 调用的驱动程序*DpWmiSetDataItem*到进程例程[ **IRP\_MN\_更改\_单一\_项**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)请求。

-   [*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)—(Optional) 启用和禁用块注册为成本高昂，若要收集的事件通知和数据收集。 WMI 调用驾*DpWmiFunctionControl*到进程例程[ **IRP\_MN\_启用\_集合**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)， [**IRP\_MN\_禁用\_集合**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)， [ **IRP\_MN\_启用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)，或[ **IRP\_MN\_禁用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)请求。

-   [*DpWmiExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_execute_method_callback)—(Optional) 执行与数据块关联的方法。 WMI 调用驾*DpWmiExecuteMethod*到进程例程[ **IRP\_MN\_EXECUTE\_方法**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)请求。

驱动程序的*DpWmiXxx*例程可以有选择的驱动程序编写器的任何名称。

然后再调用[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，该驱动程序必须初始化[ **WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)条目的结构指向其*DpWmiXxx*例程和有关其数据块和事件块的信息。

当驱动程序收到的 WMI 请求：

1. 驱动程序调用**WmiSystemControl**用一个指针指向其初始化**WMILIB\_上下文**结构、 为其设备对象的指针和指向 IRP 的指针。

2. WMI 验证 IRP 参数和调用的驱动程序*DpWmiXxx*处理请求的例程。 如果该驱动程序中设置没有入口点及其**WMILIB\_上下文**可选*DpWmiXxx*例程，WMI 完成 IRP 用默认值和状态。

3. 在其*DpWmiXxx*例程，该驱动程序处理请求并将任何输出写入到调用方提供缓冲区。 例如，驱动程序的[ *DpWmiQueryDataBlock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)例程将指定的块的请求的实例写入到缓冲区。

4. 在所有*DpWmiXxx*之外例程[ *DpWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)，驱动程序调用[ **WmiCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmicompleterequest)以完成请求，则返回状态\_推迟完成时，与任何 IRP 的待决。

5. WMI 执行任何必要的后续处理时，包中相应的任何输出**WNODE\_* XXX*** 结构，并将输出和状态传递给数据使用者。

 

 




