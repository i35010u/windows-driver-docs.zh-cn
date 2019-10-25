---
title: 电池微型类驱动程序的 DispatchSystemControl 例程
description: 电池微型类驱动程序的 DispatchSystemControl 例程
ms.assetid: bb9bb04e-4284-4e9c-85ea-60f99a01d7d9
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- DispatchSystemControl 例程
- WMI WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26d4795a016934e4a895395a4560753edc1ac5ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829912"
---
# <a name="dispatchsystemcontrol-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 DispatchSystemControl 例程


## <span id="ddk_dispatchsystemcontrol_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DISPATCHSYSTEMCONTROL_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


电池 miniclass 驱动程序必须支持[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) （WMI），方法是提供[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程来处理[**irp\_MJ\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)IRP。 WMI 为驱动程序提供了一种统一的方法来公开度量和检测数据。

电池 miniclass 驱动程序使用[**BatteryClassSystemControl**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclasssystemcontrol)例程执行初始处理。 **BatteryClassSystemControl**使用*WmiLibContext*参数，该参数指定函数的调度表。 例程使用 IRP\_MJ\_SYSTEM\_控制的**MinorFunction**成员来确定它调用哪个调度函数。

所有电池驱动程序都必须处理特定的 WMI 查询。 电池 miniclass 驱动程序无需直接支持这些 WMI 查询，而是将它们转发给电池类驱动程序以进行处理。 为了处理 WMI 查询，miniclass 驱动程序提供了指向[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)的**QueryWmiDataBlock**成员中[**DpWmiQueryDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程的指针。 不需要 miniclass 驱动程序来处理任何其他类型的 WMI 请求。 如果不是，则驱动程序将\_WMILIB 的其他成员设置为零。

在其[**DpWmiQueryDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程内，miniclass 驱动程序调用[**BatteryClassQueryWmiDataBlock**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassquerywmidatablock)例程，以允许电池类驱动程序处理 WMI 查询请求（如果可能）。 如果电池类驱动程序处理该 WMI 类 GUID，它将完成 IRP。 否则， **BatteryClassQueryWmiDataBlock**将返回\_WMI\_GUID\_不\_找到的状态值。 然后，miniclass 驱动程序可以执行其特定于驱动程序的处理，并使用[**WmiCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmicompleterequest)来完成请求。

在调用**BatteryClassQueryWmiDataBlock**后，不需要使用电池 miniclass 驱动程序执行任何 WMI IRP 处理。 对于电池 miniclass 驱动程序的 WMI 处理的最小实现，如果**BatteryClassQueryWmiDataBlock**返回状态\_WMI\_GUID\_找不到\_，则 miniclass 驱动程序只调用[**WmiCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmicompleterequest)对于 "状态" 值为 "状态"\_WMI\_GUID\_找不到\_。

 

 




