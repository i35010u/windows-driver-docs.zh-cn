---
title: UEFI 显示器电源状态协议
description: UEFI 显示器电源状态协议
ms.assetid: ab16c548-1402-4819-9fbb-a1d6f55d934a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db59ebd78497c04b6db27b85cce692e85835139c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337396"
---
# <a name="uefi-display-power-state-protocol"></a>UEFI 显示器电源状态协议


**请注意**  本部分中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

显示电源状态协议是 Microsoft UEFI 电池充电应用程序用于 UEFI 电池充电驱动程序与通信，以执行以下任务：

-   关闭屏幕，并在 10 秒显示交替低水平电量电池 UI，而无需任何用户输入后计费模式的电池电量不足期间背景光。

-   屏幕和背景光重新打开期间按下电源按钮时计费模式的电池电量不足。

**重要**  如果设备使用自定义 UEFI 电池充电而不是由 Microsoft 提供的应用程序的应用程序，UEFI 电池充电驱动程序必须实现此协议。 Windows 启动管理器将加载 Microsoft UEFI 电池充电应用程序，如果该驱动程序实现此协议。

 

有关由 Microsoft 提供的 UEFI 电池充电应用程序的详细信息，请参阅[启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

## <a name="protocol-interface"></a>协议接口


-   [EFI\_DISPLAY\_电源\_协议](efi-display-power-protocol.md)

-   [EFI\_DISPLAY\_POWER\_PROTOCOL.SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)

-   [EFI\_DISPLAY\_POWER\_PROTOCOL.GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)

-   [EFI\_DISPLAY\_POWER\_STATE](efi-display-power-state.md)

## <a name="related-topics"></a>相关主题
[UEFI 电池充电应用程序的体系结构](architecture-of-the-uefi-battery-charging-application.md)  



