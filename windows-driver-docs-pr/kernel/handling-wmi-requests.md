---
title: 处理 WMI 请求
description: 处理 WMI 请求
ms.assetid: d95b736c-045d-4888-8bab-b0a6201f8830
keywords:
- WMI WDK 内核请求
- 请求 WDK WMI
- Irp WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86fbf1fdf8ed7c07fda0f07ff13121affb5dde02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546250"
---
# <a name="handling-wmi-requests"></a>处理 WMI 请求





所有驱动程序必须设置的调度表入口点[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程来处理 WMI 请求。 如果驱动程序[将注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)，它必须处理所有的 WMI 请求。 否则，该驱动程序必须转发到下一个较低的驱动程序的所有 WMI 请求。

所有 WMI Irp 都具有重大的代码[ **IRP\_MJ\_系统\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550813)和一个次要的以下代码：

-   [**IRP\_MN\_REGINFO**](irp-mn-reginfo.md)， [ **IRP\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md)— 查询或更新的驱动程序注册信息后，驱动程序已调用[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)。

-   [**IRP\_MN\_查询\_所有\_数据**](irp-mn-query-all-data.md)， [ **IRP\_MN\_查询\_单一\_实例**](irp-mn-query-single-instance.md)— 对给定的数据块的单个实例或所有实例的查询。

-   [**IRP\_MN\_更改\_单个\_项**](irp-mn-change-single-item.md)， [ **IRP\_MN\_更改\_单\_实例**](irp-mn-change-single-instance.md)— 请求要更改单个项或多个项的数据块的实例中的驱动程序。

-   [**IRP\_MN\_启用\_集合**](irp-mn-enable-collection.md)， [ **IRP\_MN\_禁用\_集合**](irp-mn-disable-collection.md)-请求驱动程序开始累积的块的驱动程序注册为以收集，也可以停止此类块的数据的累积成本高昂的数据。

-   [**IRP\_MN\_启用\_事件**](irp-mn-enable-events.md)， [ **IRP\_MN\_禁用\_事件**](irp-mn-disable-events.md)-请求驱动程序中开始发送给定事件的通知，如果启用，发生该事件，或停止发送此类事件的通知。

-   [**IRP\_MN\_EXECUTE\_方法**](irp-mn-execute-method.md)— 请求驱动程序来执行与数据块关联的方法。

WMI 内核模式组件发送的 WMI Irp 任何时间驱动程序的成功注册为 WMI 数据提供程序，通常当用户模式下的数据使用者已请求驱动程序的设备的 WMI 信息。 如果驱动程序将注册为 WMI 数据提供程序通过调用[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)，它必须通过以下方式之一来处理每个后续的 WMI 请求：

-   调用内核模式 WMI 库例程**WmiSystemControl** PDO。 有关详细信息，请参阅[处理 WMI Irp 到调用 WmiSystemControl](calling-wmisystemcontrol-to-handle-wmi-irps.md)。

-   在其[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程，处理和完成其驱动程序对其调用中传递的设备对象的指针使用标记的任何此类请求**IoWMIRegistrationControl**，并将转发另[ **IRP\_MJ\_系统\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550813)到下一个较低的驱动程序的请求。 有关详细信息，请参阅[DispatchSystemControl 例程中处理 WMI Irp](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)。

有关 WMI 次要 Irp 的列表，请参阅[WMI 次要 Irp](wmi-minor-irps.md)。 

 




