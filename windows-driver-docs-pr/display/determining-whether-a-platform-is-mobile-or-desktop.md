---
title: 确定平台是移动平台还是桌面平台
description: 确定平台是移动平台还是桌面平台
keywords:
- TMM WDK 显示，确定移动或桌面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 930f76c7ff274908a158a2bc3d86b3ae83e35303
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809513"
---
# <a name="determining-whether-a-platform-is-mobile-or-desktop"></a>确定平台是移动平台还是桌面平台


TMM 仅在移动计算机上运行，在台式计算机上自动禁用。 硬件供应商应该启用并使用自己的专有方法，在台式计算机上输入克隆视图。 他们应该确定平台是否为移动设备，以便它们可以避免使用其专用方法在移动计算机上输入克隆视图，并使用 TMM。

硬件供应商可以使用以下代码来确定平台是移动版还是桌面版。 然后，平台可以使用适当的机制来输入克隆视图。

```cpp
#include <Powrprof.h>   // For GetPwrCapabilities

    BOOL IsMobilePlatform()
    {
        BOOL fIsMobilePlatform = FALSE;

        fIsMobilePlatform = (PlatformRoleMobile == PowerDeterminePlatformRole());

        POWER_PLATFORM_ROLE iRole;

        // Check if the operating system determines 
        // that the computer is a mobile computer.
        iRole = PowerDeterminePlatformRole();

        if (PlatformRoleMobile == iRole)
        {
            fIsMobilePlatform = TRUE;
        }
        else if (PlatformRoleDesktop == iRole) 
        // Can happen when a battery is not plugged into a laptop
        {
            SYSTEM_POWER_CAPABILITIES powerCapabilities;

            if (GetPwrCapabilities(&powerCapabilities))
            {
         // Check if a battery exists, and it is not for a UPS.
         // Note that SystemBatteriesPresent is set on a laptop even if the battery is unplugged.
                fIsMobilePlatform = ((TRUE == powerCapabilities.SystemBatteriesPresent) && (FALSE == powerCapabilities.BatteriesAreShortTerm));
            }
            // GetPwrCapabilities should never fail 
            // However, if it does, leave fReturn == FALSE.
        }

        return fIsMobilePlatform;
    }
```

有关在前面的代码中调用的函数的信息，请参阅 Microsoft Windows SDK 文档。

 

 





