---
title: UEFI 电池充电协议
description: UEFI 电池充电协议
ms.assetid: 5e9ef620-2ca1-4579-a715-19eec8933d57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dbc2d4e762a55196407854999932cd51370abb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569298"
---
# <a name="uefi-battery-charging-protocol"></a>UEFI 电池充电协议


**请注意**  本部分中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

Microsoft UEFI 电池充电应用程序使用 UEFI 电池充电协议与 UEFI 电池充电驱动程序进行通信。 UEFI 电池充电驱动程序必须实现此协议，如果设备使用 Microsoft UEFI 电池充电应用程序。

**重要**  如果设备使用自定义 UEFI 电池充电而不是由 Microsoft 提供的应用程序的应用程序，UEFI 电池充电驱动程序必须实现此协议。 Windows 启动管理器将加载 Microsoft UEFI 电池充电应用程序，如果该驱动程序实现此协议。

 

有关 Microsoft UEFI 电池充电应用程序的详细信息，请参阅[启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

## <a name="protocol-interface"></a>协议接口


-   [EFI\_电池\_正在充电\_协议](efi-battery-charging-protocol.md)

-   [EFI\_BATTERY\_CHARGING\_PROTOCOL.GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)

-   [EFI\_BATTERY\_CHARGING\_PROTOCOL.GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)

-   [EFI\_BATTERY\_CHARGING\_PROTOCOL.ChargeBattery](efi-battery-charging-protocolchargebattery.md)

Windows 启动流需要电池，它可以加载主操作系统之前向某一级别收取费用。 UEFI 规范版本 2.3 缺少标准电池充电协议。

### <a name="sequence-diagram"></a>序列图

![uefi 电池充电序列图](images/uefibatterychargingsequencediagram.png)

 

 




