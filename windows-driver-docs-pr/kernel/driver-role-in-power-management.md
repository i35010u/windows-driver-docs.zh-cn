---
title: 中电源管理的驱动程序角色
description: 中电源管理的驱动程序角色
ms.assetid: 24b55880-e767-4f18-977e-c4a93332b909
keywords:
- 电源管理 WDK 内核，驱动程序中的角色
- 系统电源状态 WDK 内核，驱动程序角色
- 设备电源状态 WDK 内核
- 驱动程序 power 支持角色 WDk 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44a8f19f06ebaf779ba8015659ebe27e65ec71d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533263"
---
# <a name="driver-role-in-power-management"></a>中电源管理的驱动程序角色





驱动程序支持电源管理两种方式：

1.  驱动程序发出的电源管理器的系统级 power 请求响应。

2.  驱动程序管理功能和性能其每个设备的状态。

每个驱动程序必须具有[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程来处理[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)请求。 *DispatchPower*例程必须检查每个 power IRP 和是对其进行处理或将其传递到下一步低驱动程序。

对于参与电源管理设备，设备在设备堆栈中的每个驱动程序必须响应或相应地将 power Irp 传递。 单个驱动程序进行正确操作可能导致禁用跨整个系统的电源管理。

对于每个设备驱动程序[管理的电源策略](managing-device-power-policy.md)其设备。 该驱动程序可以将 power Irp 发送到其自己的设备堆栈执行其设备上的电源操作。 电源策略管理器负责向系统电源 Irp 发出设备电源相对应的 Irp。

此外，驱动程序可能会执行某些 power 任务，例如在启动时在设备上启动或关闭在删除后，设备而不会收到 power IRP 的电源。 这些地址被视为隐式电源请求。

有关详细信息，请参阅[驱动程序的电源管理责任](power-management-responsibilities-for-drivers.md)。

 

 




