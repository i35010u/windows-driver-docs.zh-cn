---
title: DispatchSystemControl Routine 电池 Miniclass 驱动程序
description: DispatchSystemControl Routine 电池 Miniclass 驱动程序
ms.assetid: bb9bb04e-4284-4e9c-85ea-60f99a01d7d9
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- DispatchSystemControl 例程
- WMI WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b32abd24c8dfe06a7423225ac577f1028f9bac3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541501"
---
# <a name="dispatchsystemcontrol-routine-of-a-battery-miniclass-driver"></a>DispatchSystemControl Routine 电池 Miniclass 驱动程序


## <span id="ddk_dispatchsystemcontrol_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DISPATCHSYSTEMCONTROL_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


电池 miniclass 驱动程序必须支持[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI) 通过提供[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程来处理[ **IRP\_MJ\_系统\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550813) IRP。 WMI 提供了统一的方式公开度量和检测数据的驱动程序。

电池 miniclass 驱动程序使用[ **BatteryClassSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff536270)例程，以执行初始化处理。 **BatteryClassSystemControl**采用*WmiLibContext*参数，它指定的函数调度表。 例程使用**MinorFunction** IRP 的成员\_MJ\_系统\_控件来确定哪些调度函数它调用。

没有电池设备的所有驱动程序必须处理某些 WMI 查询。 电池 miniclass 驱动程序不需要这些 WMI 查询直接支持，但改为将其转发到电池类驱动程序来处理。 若要处理 WMI 查询，miniclass 驱动程序提供一个指针指向[ **DpWmiQueryDataBlock** ](https://msdn.microsoft.com/library/windows/hardware/ff544096)例程中**QueryWmiDataBlock**隶属[ **WMILIB\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff565813)。 Miniclass 驱动程序不需要处理任何其他类型的 WMI 请求。 如果未显示，驱动程序设置的其他成员 WMILIB\_上下文为零。

在其[ **DpWmiQueryDataBlock** ](https://msdn.microsoft.com/library/windows/hardware/ff544096)例程，miniclass 驱动程序调用[ **BatteryClassQueryWmiDataBlock** ](https://msdn.microsoft.com/library/windows/hardware/ff536268)到例程允许以处理 WMI 查询请求，如果它可以在电池类驱动程序。 如果电池类驱动程序处理的 WMI 类 GUID，它将完成 IRP。 否则为**BatteryClassQueryWmiDataBlock**返回的值为状态\_WMI\_GUID\_不\_找到。 然后，miniclass 驱动程序可以进行特定于驱动程序处理，并使用[ **WmiCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff565798)来完成该请求。

电池 miniclass 驱动程序不需要执行处理超出调用任何 WMI IRP **BatteryClassQueryWmiDataBlock**。 在 WMI 电池 miniclass 驱动程序，如果处理的最小实现**BatteryClassQueryWmiDataBlock**将返回状态\_WMI\_GUID\_不\_找到，miniclass驱动程序只需调用[ **WmiCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff565798)状态将 status 值\_WMI\_GUID\_不\_找到。

 

 




