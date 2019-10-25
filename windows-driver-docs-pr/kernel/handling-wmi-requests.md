---
title: 处理 WMI 请求
description: 处理 WMI 请求
ms.assetid: d95b736c-045d-4888-8bab-b0a6201f8830
keywords:
- WMI WDK 内核，请求
- 请求 WDK WMI
- Irp WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fd1080ce6c5df2a2abb6ba99e4290b0bf192f29
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838651"
---
# <a name="handling-wmi-requests"></a>处理 WMI 请求





所有驱动程序都必须设置调度表入口点， [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程才能处理 WMI 请求。 如果驱动程序[注册为 wmi 数据提供程序](registering-as-a-wmi-data-provider.md)，则它必须处理所有 WMI 请求。 否则，驱动程序必须将所有 WMI 请求转发到下一个较低的驱动程序。

所有 WMI Irp 都具有主要的代码[**IRP\_MJ\_SYSTEM\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)和以下次要代码之一：

-   [**Irp\_MN\_REGINFO**](irp-mn-reginfo.md)， [**irp\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md)）驱动程序调用[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)后，查询或更新驱动程序的注册信息。

-   [**Irp\_MN\_query\_所有\_数据**](irp-mn-query-all-data.md)、 [**IRP\_MN\_查询\_单\_实例**](irp-mn-query-single-instance.md)-查询所有实例或给定数据块的单个实例。

-   [**Irp\_MN\_更改\_单一\_项**](irp-mn-change-single-item.md)、 [**IRP\_MN\_更改\_单个\_实例**](irp-mn-change-single-instance.md)-请求驱动程序更改数据块实例中的单个项或多个项。

-   [**Irp\_MN\_启用\_收集**](irp-mn-enable-collection.md)， [**IRP\_MN\_禁用\_收集**](irp-mn-disable-collection.md)-请求驱动程序开始为驱动程序已注册为收集或停止的块收集数据此类块的累计数据。

-   [**Irp\_MN\_启用\_事件**](irp-mn-enable-events.md)， [**IRP\_MN\_禁用\_事件**](irp-mn-disable-events.md)-请求驱动程序在该事件发生时开始发送给定事件的通知，或者停止发送通知此类事件。

-   [**IRP\_MN\_执行\_方法**](irp-mn-execute-method.md)-请求驱动程序执行与数据块关联的方法。

WMI 内核模式组件在驱动程序成功注册为 WMI 数据提供程序的任何时候都发送 WMI Irp，通常在用户模式数据使用者为驱动程序的设备请求 WMI 信息时发送。 如果驱动程序通过调用[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)注册为 WMI 数据提供程序，则它必须通过以下方式之一来处理每个后续 WMI 请求：

-   调用 PDO 的内核模式 WMI 库例程**WmiSystemControl** 。 有关详细信息，请参阅[调用 WmiSystemControl 来处理 WMI irp](calling-wmisystemcontrol-to-handle-wmi-irps.md)。

-   在[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中，处理并完成用指针标记的任何此类请求，该指针指向驱动程序在其对**IoWMIRegistrationControl**的调用中传递的设备对象，并转发其他[**IRP\_MJ\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)对下一个较低驱动程序的请求。 有关详细信息，请参阅[在 DispatchSystemControl 例程中处理 WMI irp](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)。

有关 WMI 次要 Irp 的列表，请参阅[Wmi 次要 irp](wmi-minor-irps.md)。 

 




