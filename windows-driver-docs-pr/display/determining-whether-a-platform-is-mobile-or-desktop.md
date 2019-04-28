---
title: 确定平台是移动平台还是桌面平台
description: 确定平台是移动平台还是桌面平台
ms.assetid: f0a553a4-a23b-45c8-abc5-b5014ba328ae
keywords:
- TMM WDK 显示、 确定移动或桌面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 420f26fddec527b63c539a6adfc647d6b8034f44
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342423"
---
# <a name="determining-whether-a-platform-is-mobile-or-desktop"></a>确定平台是移动平台还是桌面平台


TMM 仅在移动计算机上运行，并自动在台式计算机上禁用。 硬件供应商应启用并使用自己专有的方法来输入台式计算机上的克隆视图。 它们应确定一个平台，以便它们可以避免使用其专有方法来输入移动计算机上的克隆视图，并改为使用 TMM 是移动。

硬件供应商可以使用以下代码以确定平台是否移动或桌面。 然后，平台可用的适当机制来输入克隆视图。

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

有关在上述代码中调用的函数的信息，请参阅 Microsoft Windows SDK 文档。

 

 





