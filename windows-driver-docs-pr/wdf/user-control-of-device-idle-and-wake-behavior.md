---
title: 设备空闲和唤醒行为的用户控件
description: 设备空闲和唤醒行为的用户控件
ms.assetid: 776fcf82-2235-489a-8d46-3ad230da3402
keywords:
- 系统唤醒 KMDF
- 电源管理 WDK KMDF、唤醒功能
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 低功耗状态 WDK KMDF
- 电源管理 WDK KMDF、空闲关机
- 空闲的关闭 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a3c3c0b22f893697546ee50e20dd8b237b603ea
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185053"
---
# <a name="user-control-of-device-idle-and-wake-behavior"></a>设备空闲和唤醒行为的用户控件


如果设备具有空闲关机或唤醒功能，你可以决定是否允许用户启用或禁用这些功能。

你的驱动程序可以使用 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings) 结构的成员来指定具有注册表访问权限的用户是否可以启用或禁用设备的空闲电源功能。

你的驱动程序可以使用 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 唤醒 \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings) 结构的成员来指定具有注册表访问权限的用户是否可以启用或禁用设备的唤醒功能。

这两个结构都允许驱动程序启用功能，禁用功能，或使用户能够控制功能。 为了使用户能够控制，在适当的设置结构中，驱动程序将 **UserControlOfIdleSettings** 或 **UserControlOfWakeSettings** 成员分别设置为 **IdleAllowUserControl** 或 **WakeAllowUserControl**，并将 **Enabled** 成员设置为 **WdfTrue** 或 **WdfUseDefault**。

如果你的驱动程序允许用户修改空闲和唤醒设置，则该框架将以设备管理器显示的属性表页面的形式提供用户界面，以便用户可以启用或禁用空闲和唤醒功能。  (框架修改 **IdleInWorkingState** 和 **WakeFromSleepState** 注册表值。 驱动程序及其安装文件 *不* 能读取或修改这些值。 ) 

如果用户修改设备的设置，则在必要时，框架会更新设备的电源状态以匹配新的设置。 例如，如果用户在设备处于空闲状态时禁用了设备的空闲关机功能，则该框架会将设备返回到其工作状态。

如果你的驱动程序允许用户修改空闲和唤醒设置，则默认情况下，框架将启用这些设置。 某些驱动程序编写器在允许用户修改这些设置之前，可能需要先禁用这些设置。

因此，对于版本1.9 及更高版本的 KMDF，该框架提供了两个驱动程序可定义的注册表值（名为 **WdfDefaultIdleInWorkingState** 和 **WdfDefaultWakeFromSleepState**），这些值存储在设备的硬件密钥下的设备的 **设备参数 \\ WDF** 子项中。 值为 REG \_ DWORD 类型，其中 "0" 指示禁用功能，"1" 表示已启用该功能。

驱动程序的 INF 文件可使用 [**INF AddReg 指令**](../install/inf-addreg-directive.md) 创建和设置 **WdfDefaultIdleInWorkingState** 和 **WdfDefaultWakeFromSleepState** 注册表值。 例如，如果你的驱动程序启用了设备的空闲关机功能，但如果在安装设备时必须禁用该功能，则驱动程序的 INF 文件可以将 **WdfDefaultIdleInWorkingState** 设置为 "0"。

仅当驱动程序已将**UserControlOfIdleSettings**或**UserControlOfWakeSettings**成员分别设置为**IdleAllowUserControl**或**WakeAllowUserControl**，并在适当的设置结构中将**Enabled**成员设置为**WdfTrue**或**WdfUseDefault**时，框架才会检查**WdfDefaultIdleInWorkingState**和**WdfDefaultWakeFromSleepState**注册表值。

 

