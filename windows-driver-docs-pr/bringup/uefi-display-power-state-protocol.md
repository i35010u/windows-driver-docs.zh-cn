---
title: UEFI 显示器电源状态协议
description: UEFI 显示器电源状态协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6f43048542e40b5605015fab345fd198f5b5ba0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803639"
---
# <a name="uefi-display-power-state-protocol"></a>UEFI 显示器电源状态协议


**注意**  本节中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

显示电源状态协议由 Microsoft UEFI 电池充电应用程序用来与 UEFI 电池充电驱动程序通信，以便执行以下任务：

-   在无需任何用户输入的情况下，在不使用任何用户输入的情况下，在不使用任何用户输入的情况下显示10秒的备用电池使用情况

-   按下电源按钮时，请在电池充电模式低时打开屏幕和背景光。

**重要提示**  如果设备使用自定义的 UEFI 电池充电应用程序而不是 Microsoft 提供的应用程序，则 UEFI 电池充电驱动程序不得实现此协议。 如果驱动程序实现此协议，Windows 启动管理器将加载 Microsoft UEFI 电池充电应用程序。

 

有关 Microsoft 提供的 UEFI 电池充电应用程序的详细信息，请参阅 [启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

## <a name="protocol-interface"></a>协议接口


-   [EFI \_ 显示 \_ 电源 \_ 协议](efi-display-power-protocol.md)

-   [EFI \_ 显示 \_ 电源 \_ 协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)

-   [EFI \_ 显示 \_ 电源 \_ 协议。GetDisplayPowerState](efi-display-power-protocolgetdisplaypowerstate.md)

-   [EFI \_ 显示 \_ 电源 \_ 状态](efi-display-power-state.md)

## <a name="related-topics"></a>相关主题
[UEFI 电池充电应用程序的体系结构](architecture-of-the-uefi-battery-charging-application.md)  



