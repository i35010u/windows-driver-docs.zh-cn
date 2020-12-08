---
title: UMDF 中设备空闲和唤醒行为的用户控件
description: UMDF 中设备空闲和唤醒行为的用户控件
keywords:
- 电源管理 WDK UMDF，空闲关机
- 电源管理 WDK UMDF，唤醒
- 空闲电源关闭功能 WDK UMDF
- 空闲电源关闭功能 WDK UMDF，用户控制
- 唤醒功能 WDK UMDF
- 唤醒功能 WDK UMDF，用户控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 385c711f9c76da40ec65313347730f299632ee59
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824843"
---
# <a name="user-control-of-device-idle-and-wake-behavior-in-umdf"></a>UMDF 中设备空闲和唤醒行为的用户控件


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果设备具有空闲关机或唤醒功能，你可以决定是否允许用户启用或禁用这些功能。

基于 UMDF 的驱动程序可以使用 [**IWDFDevice2：： AssignS0IdleSettings**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings) 方法来指定具有注册表访问权限的用户是否可以启用或禁用设备的空闲电源关闭功能。

你的驱动程序可以使用 [**IWDFDevice2：： AssignSxWakeSettings**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings) 方法来指定具有注册表访问权限的用户是否可以启用或禁用设备的唤醒功能。

这两种方法都允许驱动程序启用功能，禁用功能，或使用户能够控制功能：

-   当驱动程序调用 **AssignS0IdleSettings** 方法时，它可以通过将 *UserControlOfIdleSettings* 参数设置为 **IdleAllowUserControl** 并将 *Enabled* 参数设置为 **WdfTrue** 或 **WdfUseDefault**，使用户控制设备的空闲功能。

-   当驱动程序调用 **AssignSxWakeSettings** 方法时，它可以通过将 *UserControlOfWakeSettings* 参数设置为 **WakeAllowUserControl** 并将 *Enabled* 参数设置为 **WdfTrue** 或 **WdfUseDefault**，使用户控制设备的唤醒功能。

如果你的驱动程序允许用户修改空闲和唤醒设置，则该框架将以设备管理器显示的属性表页面的形式提供用户界面，以便用户可以启用或禁用空闲和唤醒功能。  (框架修改 **IdleInWorkingState** 和 **WakeFromSleepState** 注册表值。 驱动程序及其安装文件不能读取或修改这些值。 ) 

如果用户修改设备的设置，则在必要时，框架会更新设备的电源状态以匹配新的设置。 例如，如果用户在设备处于空闲状态时禁用了设备的空闲关机功能，则该框架会将设备返回到其工作状态。

如果你的驱动程序允许用户修改空闲和唤醒设置，则默认情况下，框架将启用这些设置。 某些驱动程序编写器在允许用户修改这些设置之前，可能需要先禁用这些设置。

因此，framework 版本1.9 和更高版本提供了两个驱动程序可定义的注册表值（名为 **WdfDefaultIdleInWorkingState** 和 **WdfDefaultWakeFromSleepState**），这些值存储在设备的 [硬件密钥](./using-the-registry-in-umdf-1-x-drivers.md)下的设备的 **设备参数 \\ WDF** 子项中。 值为 REG \_ DWORD 类型，其中 "0" 指示禁用功能，"1" 表示已启用该功能。

驱动程序的 INF 文件可使用 [**INF AddReg 指令**](../install/inf-addreg-directive.md) 创建和设置 **WdfDefaultIdleInWorkingState** 和 **WdfDefaultWakeFromSleepState** 注册表值。 例如，如果你的驱动程序启用了设备的空闲关机功能，但如果在安装设备时必须禁用该功能，则驱动程序的 INF 文件可以将 **WdfDefaultIdleInWorkingState** 设置为 "0"。

仅当驱动程序调用 [**WdfUseDefault：： IWDFDevice2**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)方法时，驱动程序将 *UserControlOfIdleSettings* 参数设置为 **IdleAllowUserControl** ，并将 *Enabled* 参数设置为 **WdfTrue** 或 **AssignS0IdleSettings** 时，框架才会检查 **WdfDefaultIdleInWorkingState** 注册表值。

仅当驱动程序调用 [**WdfUseDefault：： IWDFDevice2**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)方法时，驱动程序将 *UserControlOfWakeSettings* 参数设置为 **IWakeAllowUserControl** ，并将 *Enabled* 参数设置为 **WdfTrue** 或 **AssignSxWakeSettings** 时，框架才会检查 **WdfDefaultWakeFromSleepState** 注册表值。

 

