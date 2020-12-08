---
title: UEFI 电池充电协议
description: UEFI 电池充电协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 400ffcb8499ca77d9aceb2907d5cb27a8fd94631
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803647"
---
# <a name="uefi-battery-charging-protocol"></a>UEFI 电池充电协议


**注意**  本节中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

Microsoft UEFI 电池充电应用程序使用 UEFI 电池充电协议与 UEFI 电池充电驱动程序通信。 如果设备使用 Microsoft UEFI 电池充电应用程序，则 UEFI 充电驱动程序必须实现此协议。

**重要提示**  如果设备使用自定义的 UEFI 电池充电应用程序而不是 Microsoft 提供的应用程序，则 UEFI 电池充电驱动程序不得实现此协议。 如果驱动程序实现此协议，Windows 启动管理器将加载 Microsoft UEFI 电池充电应用程序。

 

有关 Microsoft UEFI 电池充电应用程序的详细信息，请参阅 [启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

## <a name="protocol-interface"></a>协议接口


-   [EFI \_ 电池 \_ 充电 \_ 协议](efi-battery-charging-protocol.md)

-   [EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)

-   [EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)

-   [EFI \_ 电池 \_ 充电 \_ 协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)

Windows 启动流要求在将电池加载到主 OS 之前，将电池计费到特定级别。 UEFI 规范版本2.3 缺少标准的电池充电协议。

### <a name="sequence-diagram"></a>序列图

![uefi 电池充电序列图](images/uefibatterychargingsequencediagram.png)

 

 




