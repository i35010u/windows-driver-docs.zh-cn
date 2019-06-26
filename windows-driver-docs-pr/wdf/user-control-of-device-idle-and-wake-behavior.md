---
title: 设备空闲和唤醒行为的用户控件
description: 设备空闲和唤醒行为的用户控件
ms.assetid: 776fcf82-2235-489a-8d46-3ad230da3402
keywords:
- 系统唤醒 WDK KMDF
- 电源管理 WDK KMDF，唤醒功能
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 低功耗状态 WDK KMDF
- 电源管理 WDK KMDF、 空闲关机
- 空闲关闭 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4476176720a36c6567b219c61312fa3b80f1fa62
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372293"
---
# <a name="user-control-of-device-idle-and-wake-behavior"></a>设备空闲和唤醒行为的用户控件


如果设备具有空闲断电或唤醒功能，可以决定是否应允许用户启用或禁用这些功能。

您的驱动程序可以使用的成员[ **WDF\_设备\_POWER\_策略\_空闲\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构，以指定是否具有注册表访问权限的用户可以启用或禁用设备的空闲电源关闭功能。

您的驱动程序可以使用的成员[ **WDF\_设备\_POWER\_策略\_唤醒\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)结构，以指定是否具有注册表访问权限的用户可以启用或禁用设备的唤醒功能。

同时的这些结构允许以启用功能，该驱动程序禁用功能，或为用户提供的功能的控件。 若要为用户提供控制，请在相应的设置结构，该驱动程序设置**UserControlOfIdleSettings**或**UserControlOfWakeSettings**成员添加到**IdleAllowUserControl**或**WakeAllowUserControl**分别，和**已启用**成员添加到**WdfTrue**或**WdfUseDefault**,.

如果您的驱动程序允许用户修改空闲状态并唤醒设置，该框架提供用户界面，在设备管理器显示，以便用户可以启用或禁用空闲和唤醒功能的属性表页的窗体中。 (框架修改**IdleInWorkingState**并**WakeFromSleepState**注册表值。 驱动程序和其安装文件必须*不*读取或修改这些值。)

如果用户修改设备的设置，该框架将更新设备的电源状态以匹配新的设置，如有必要。 例如，如果用户禁用设备的空闲关机功能已，而设备在低功耗状态中因为它处于闲置状态，该框架将设备返回到其工作状态。

如果您的驱动程序允许用户修改空闲状态并唤醒设置，该框架会默认启用这些设置。 某些驱动程序编写人员可能想要允许用户对其进行修改之前最初禁用的设置。

因此，对于 1.9 版和更高版本的 KMDF，框架提供了两个驱动程序可定义的注册表值，名为**WdfDefaultIdleInWorkingState**并**WdfDefaultWakeFromSleepState**，这存储在设备的**设备参数\\WDF**子项，请在设备的硬件密钥。 值是 REG\_DWORD 类型，与"0"，该值指示功能已禁用和启用了"1"，该值指示该功能。

可以使用驱动程序的 INF 文件[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)创建并设置**WdfDefaultIdleInWorkingState**和**WdfDefaultWakeFromSleepState**注册表值。 例如，如果您的驱动程序启用设备的空闲电源关闭功能，但如果安装设备时，必须禁用该功能，可以设置驱动程序的 INF 文件**WdfDefaultIdleInWorkingState**为"0"。

该框架将检查**WdfDefaultIdleInWorkingState**并**WdfDefaultWakeFromSleepState**注册表值已设置该驱动程序才**UserControlOfIdleSettings**或**UserControlOfWakeSettings**成员添加到**IdleAllowUserControl**或**WakeAllowUserControl**分别，并且**已启用**成员添加到**WdfTrue**或**WdfUseDefault**，相应的设置结构中。

 

 





