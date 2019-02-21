---
title: 设备的用户控制空闲和唤醒 UMDF 中的行为
description: 设备的用户控制空闲和唤醒 UMDF 中的行为
ms.assetid: 9341c412-dd0a-4e80-a164-250e24004082
keywords:
- 电源管理 WDK UMDF，空闲电源关闭
- 电源管理 WDK UMDF 唤醒
- 空闲关机功能 WDK UMDF
- 空闲关机功能 WDK UMDF，用户控件
- 唤醒功能 WDK UMDF
- 唤醒功能 WDK UMDF，用户控件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80ac6ca9101131ed31599c38ef425ffa5e3928f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534266"
---
# <a name="user-control-of-device-idle-and-wake-behavior-in-umdf"></a>设备的用户控制空闲和唤醒 UMDF 中的行为


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果设备具有空闲断电或唤醒功能，可以决定是否应允许用户启用或禁用这些功能。

可以使用基于 UMDF 驱动程序[ **IWDFDevice2::AssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556920)方法，以指定是否具有注册表访问权限的用户可以启用或禁用设备的空闲电源关闭功能。

可以使用您的驱动程序[ **IWDFDevice2::AssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556923)方法，以指定是否具有注册表访问权限的用户可以启用或禁用设备的唤醒功能。

同时这些方法允许以启用功能，该驱动程序禁用功能，或为用户提供的功能的控件：

-   当驱动程序调用**AssignS0IdleSettings**方法，它可以为用户提供的设备的空闲功能控制通过设置*UserControlOfIdleSettings*参数**IdleAllowUserControl**并设置*已启用*参数**WdfTrue**或**WdfUseDefault**。

-   当驱动程序调用**AssignSxWakeSettings**方法，它可以为用户提供的设备的唤醒功能的控件通过设置*UserControlOfWakeSettings*参数**WakeAllowUserControl**并设置*已启用*参数**WdfTrue**或**WdfUseDefault**。

如果您的驱动程序允许用户修改空闲状态并唤醒设置，该框架提供用户界面，在设备管理器显示，以便用户可以启用或禁用空闲和唤醒功能的属性表页的窗体中。 (框架修改**IdleInWorkingState**并**WakeFromSleepState**注册表值。 驱动程序和其安装文件必须不读取或修改这些值。）

如果用户修改设备的设置，该框架将更新设备的电源状态以匹配新的设置，如有必要。 例如，如果用户禁用设备的空闲关机功能已，而设备在低功耗状态中因为它处于闲置状态，该框架将设备返回到其工作状态。

如果您的驱动程序允许用户修改空闲状态并唤醒设置，该框架会默认启用这些设置。 某些驱动程序编写人员可能想要允许用户对其进行修改之前最初禁用的设置。

因此，版本 1.9 及更高版本的 framework 提供两个驱动程序可定义的注册表值，名为**WdfDefaultIdleInWorkingState**并**WdfDefaultWakeFromSleepState**，这存储在设备的**设备参数\\WDF**子项，请在设备下[硬件密钥](https://msdn.microsoft.com/library/windows/hardware/ff561381)。 值是 REG\_DWORD 类型，与"0"，该值指示功能已禁用和启用了"1"，该值指示该功能。

可以使用驱动程序的 INF 文件[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)创建并设置**WdfDefaultIdleInWorkingState**和**WdfDefaultWakeFromSleepState**注册表值。 例如，如果您的驱动程序启用设备的空闲电源关闭功能，但如果安装设备时，必须禁用该功能，可以设置驱动程序的 INF 文件**WdfDefaultIdleInWorkingState**为"0"。

该框架将检查**WdfDefaultIdleInWorkingState**仅当驱动程序设置的注册表值*UserControlOfIdleSettings*参数**IdleAllowUserControl**并*已启用*参数**WdfTrue**或**WdfUseDefault**当驱动程序调用[ **IWDFDevice2::AssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556920)方法。

该框架将检查**WdfDefaultWakeFromSleepState**仅当驱动程序设置的注册表值*UserControlOfWakeSettings*参数**IWakeAllowUserControl**并*已启用*参数**WdfTrue**或**WdfUseDefault**当驱动程序调用[ **IWDFDevice2::AssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556923)方法。

 

 





