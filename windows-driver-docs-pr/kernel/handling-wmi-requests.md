---
title: 处理 WMI 请求
description: 处理 WMI 请求
keywords:
- WMI WDK 内核，请求
- 请求 WDK WMI
- Irp WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b16a1823c89eadcad59115f6dc13e4ac2143fce7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836937"
---
# <a name="handling-wmi-requests"></a>处理 WMI 请求





所有驱动程序都必须设置调度表入口点， [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程才能处理 WMI 请求。 如果驱动程序 [注册为 wmi 数据提供程序](registering-as-a-wmi-data-provider.md)，则它必须处理所有 WMI 请求。 否则，驱动程序必须将所有 WMI 请求转发到下一个较低的驱动程序。

所有 WMI Irp 都具有主要的代码 [**IRP \_ MJ \_ 系统 \_ 控件**](./irp-mj-system-control.md) 和以下次要代码之一：

-   [**IRP \_MN \_ REGINFO**](irp-mn-reginfo.md)， [**IRP \_ MN \_ REGINFO \_ EX**](irp-mn-reginfo-ex.md)-在驱动程序调用 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)后，查询或更新驱动程序的注册信息。

-   [**IRP \_MN \_ 查询 \_ 所有 \_ 数据**](irp-mn-query-all-data.md)， [**IRP \_ MN \_ 查询 \_ 单 \_ 实例**](irp-mn-query-single-instance.md)-查询所有实例或给定数据块的单个实例。

-   [**IRP \_MN \_ change \_ 单一 \_ 项**](irp-mn-change-single-item.md)， [**IRP \_ MN \_ change \_ 单一 \_ 实例**](irp-mn-change-single-instance.md)-请求驱动程序更改数据块实例中的单个项或多个项。

-   [**IRP \_MN \_ 启用 \_ 收集**](irp-mn-enable-collection.md)， [**IRP \_ MN \_ 禁用 \_ 收集**](irp-mn-disable-collection.md)-请求驱动程序开始为驱动程序已注册为收集开销较高的块开始累积数据，或停止此类块的累积数据。

-   [**IRP \_MN \_ ENABLE \_ events**](irp-mn-enable-events.md)， [**IRP \_ MN \_ DISABLE \_ events**](irp-mn-disable-events.md)-请求驱动程序开始发送给定事件的通知，前提是该事件在启用后发生，或者停止发送此类事件的通知。

-   [**IRP \_MN \_ execute \_ 方法**](irp-mn-execute-method.md)-请求驱动程序执行与数据块关联的方法。

WMI 内核模式组件在驱动程序成功注册为 WMI 数据提供程序的任何时候都发送 WMI Irp，通常在用户模式数据使用者为驱动程序的设备请求 WMI 信息时发送。 如果驱动程序通过调用 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)注册为 WMI 数据提供程序，则它必须通过以下方式之一来处理每个后续 WMI 请求：

-   调用内核模式 WMI 库例程 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)。 驱动程序可以调用 **WmiSystemControl** 来处理仅涉及不使用动态实例名称的块的请求，以及基于单个基名称字符串或 PDO 的 *设备实例 ID* 的基本静态实例名称。 有关详细信息，请参阅 [调用 WmiSystemControl 来处理 WMI irp](calling-wmisystemcontrol-to-handle-wmi-irps.md)。

-   在其 [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中，处理并完成用指针标记的任何此类请求，该指针指向驱动程序在其对 **IoWMIRegistrationControl** 的调用中传递的设备对象，然后将其他 [**IRP \_ MJ \_ 系统 \_ 控制**](./irp-mj-system-control.md) 请求转发到下一个较低的驱动程序。 有关详细信息，请参阅 [在 DispatchSystemControl 例程中处理 WMI irp](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)。

有关 WMI 次要 Irp 的列表，请参阅 [Wmi 次要 irp](wmi-minor-irps.md)。 
