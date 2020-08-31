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
ms.openlocfilehash: 9ca0f43fc2c2dfbe262e8d129df368eec5d0d778
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056911"
---
# <a name="dispatchsystemcontrol-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 DispatchSystemControl 例程


## <span id="ddk_dispatchsystemcontrol_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DISPATCHSYSTEMCONTROL_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


电池 miniclass 驱动程序必须通过提供[*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程来处理[**irp \_ MJ \_ 系统 \_ 控件**](../kernel/irp-mj-system-control.md)IRP，才能支持 (WMI) [Windows Management Instrumentation](../kernel/implementing-wmi.md) 。 WMI 为驱动程序提供了一种统一的方法来公开度量和检测数据。

电池 miniclass 驱动程序使用 [**BatteryClassSystemControl**](/windows/desktop/api/batclass/nf-batclass-batteryclasssystemcontrol) 例程执行初始处理。 **BatteryClassSystemControl** 使用 *WmiLibContext* 参数，该参数指定函数的调度表。 例程使用 IRP MJ **MinorFunction**系统控件的 MinorFunction \_ 成员 \_ \_ 来确定它调用哪个调度函数。

所有电池驱动程序都必须处理特定的 WMI 查询。 电池 miniclass 驱动程序无需直接支持这些 WMI 查询，而是将它们转发给电池类驱动程序以进行处理。 为了处理 WMI 查询，miniclass 驱动程序提供了指向[**WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)的**QueryWmiDataBlock**成员中的[**DpWmiQueryDataBlock**](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程的指针。 不需要 miniclass 驱动程序来处理任何其他类型的 WMI 请求。 如果不是，则驱动程序将 WMILIB 上下文的其他成员设置 \_ 为零。

在其 [**DpWmiQueryDataBlock**](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback) 例程内，miniclass 驱动程序调用 [**BatteryClassQueryWmiDataBlock**](/windows/desktop/api/batclass/nf-batclass-batteryclassquerywmidatablock) 例程，以允许电池类驱动程序处理 WMI 查询请求（如果可能）。 如果电池类驱动程序处理该 WMI 类 GUID，它将完成 IRP。 否则， **BatteryClassQueryWmiDataBlock** 将返回 " \_ 未找到状态 WMI GUID" 的值 \_ \_ \_ 。 然后，miniclass 驱动程序可以执行其特定于驱动程序的处理，并使用 [**WmiCompleteRequest**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmicompleterequest) 来完成请求。

在调用 **BatteryClassQueryWmiDataBlock**后，不需要使用电池 miniclass 驱动程序执行任何 WMI IRP 处理。 在为电池 miniclass 驱动程序提供的 WMI 处理的最小实现中，如果**BatteryClassQueryWmiDataBlock**返回状态 \_ wmi \_ guid \_ \_ ，则 miniclass 驱动程序[**WmiCompleteRequest**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmicompleterequest)只会调用状态值为 "状态 \_ wmi \_ guid \_ 未 \_ 找到" 的 WmiCompleteRequest。

 

