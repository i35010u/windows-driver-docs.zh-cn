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
ms.openlocfilehash: 1e1d3ab76ce09e6c92c211a00a1355af6dec2f06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843106"
---
# <a name="user-control-of-device-idle-and-wake-behavior"></a>设备空闲和唤醒行为的用户控件


如果设备具有空闲关机或唤醒功能，你可以决定是否允许用户启用或禁用这些功能。

你的驱动程序可以使用[**WDF\_设备成员\_POWER\_策略\_空闲\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构来指定具有注册表访问权限的用户是否可以启用或禁用设备的空闲电源关闭功能。

你的驱动程序可以使用[**WDF\_设备成员\_POWER\_策略\_唤醒\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)结构来指定具有注册表访问权限的用户是否可以启用或禁用设备的唤醒功能。

这两个结构都允许驱动程序启用功能，禁用功能，或使用户能够控制功能。 为了使用户控制，在适当的设置结构中，驱动程序将**UserControlOfIdleSettings**或**UserControlOfWakeSettings**成员分别设置为**IdleAllowUserControl**或**WakeAllowUserControl**，并**已启用**的成员到**WdfTrue**或**WdfUseDefault**，。

如果你的驱动程序允许用户修改空闲和唤醒设置，则该框架将以设备管理器显示的属性表页面的形式提供用户界面，以便用户可以启用或禁用空闲和唤醒功能。 （框架修改**IdleInWorkingState**和**WakeFromSleepState**注册表值。 驱动程序及其安装文件*不*能读取或修改这些值。）

如果用户修改设备的设置，则在必要时，框架会更新设备的电源状态以匹配新的设置。 例如，如果用户在设备处于空闲状态时禁用了设备的空闲关机功能，则该框架会将设备返回到其工作状态。

如果你的驱动程序允许用户修改空闲和唤醒设置，则默认情况下，框架将启用这些设置。 某些驱动程序编写器在允许用户修改这些设置之前，可能需要先禁用这些设置。

因此，对于版本1.9 及更高版本的 KMDF，该框架提供了两个可由驱动程序定义的注册表值（名为**WdfDefaultIdleInWorkingState** ）和**WdfDefaultWakeFromSleepState**，它们存储在设备的**设备中参数\\** 项在设备硬件密钥下。 值为 REG\_DWORD 类型，其中 "0" 指示禁用功能，"1" 表示已启用该功能。

驱动程序的 INF 文件可使用[**INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)创建和设置**WdfDefaultIdleInWorkingState**和**WdfDefaultWakeFromSleepState**注册表值。 例如，如果你的驱动程序启用了设备的空闲关机功能，但如果在安装设备时必须禁用该功能，则驱动程序的 INF 文件可以将**WdfDefaultIdleInWorkingState**设置为 "0"。

仅当驱动程序已将**UserControlOfIdleSettings**或**UserControlOfWakeSettings**成员设置为 **时，框架才检查 WdfDefaultIdleInWorkingState 和 WdfDefaultWakeFromSleepState 注册表值**在适当的设置结构中，分别将 IdleAllowUserControl 或**WakeAllowUserControl**以及**Enabled**成员设置为**WdfTrue**或**WdfUseDefault**。

 

 





