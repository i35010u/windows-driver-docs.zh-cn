---
title: 设置保护级别
description: 设置保护级别
keywords:
- 复制保护 WDK COPP，保护级别
- 视频副本保护 WDK COPP，保护级别
- COPP WDK DirectX VA，保护级别
- 受保护的视频 WDK COPP，保护级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1eac718f270984c43c9d62b666cfc576c0a0cf37
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822459"
---
# <a name="setting-the-protection-level"></a>设置保护级别


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

COPP 命令可以设置与 DirectX VA COPP 设备关联的物理连接器上保护类型的保护级别。 若要设置保护级别，视频微型端口驱动程序的 [*COPPCommand*](./coppcommand.md) 函数接收指向 [**DXVA \_ COPPCommand**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand) 结构的指针，并将 **GUIDCOMMANDID** 成员设置为 DXVA \_ COPPSetProtectionLevel GUID，并将 **CommandData** 成员设置为指向 [**DXVA \_ COPPSetProtectionLevelCmdData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsetprotectionlevelcmddata) 结构的指针，该指针指定要设置的保护类型以及设置保护的级别。 如果保护级别不可用于保护类型，则 COPP 命令会将保护级别设置为 COPP \_ NoProtectionLevelAvailable (-1) 。 COPP 命令还可以在 DXVA COPPSetProtectionLevelCmdData 的 **ExtendedInfoChangeMask** 和 **ExtendedInfoData** 成员中指定某些扩展信息， \_ 以设置保护类型的视频微型端口驱动程序。

对于指定的保护类型，可以设置以下保护级别：

-   对于 COPP \_ ProtectionType \_ ACP，请从 **COPP \_ ACP \_ 保护 \_ 级别** 枚举类型设置以下值之一：
    -   COPP \_ ACP \_ LEVEL0 或 COPP \_ ACP \_ LevelMin (0) 
    -   COPP \_ ACP \_ 级别 1 (1) 
    -   COPP \_ ACP \_ 级别 2 (2) 
    -   COPP \_ ACP \_ 级别3或 \_ COPP \_ ACP LevelMax (3) 

<!-- -->

-   对于 COPP \_ ProtectionType \_ CGMSA，请从 **COPP \_ CGMSA \_ 保护 \_ 级别** 枚举类型设置以下值之一：
    -   \_ \_ 已禁用 COPP CGMSA 或 COPP \_ CGMSA \_ LevelMin (0) 
    -   COPP \_ CGMSA \_ CopyFreely (1) 
    -   COPP \_ CGMSA \_ CopyNoMore (2) 
    -   COPP \_ CGMSA \_ CopyOneGeneration (3) 
    -   COPP \_ CGMSA \_ CopyNever (4) 
    -   COPP \_ CGMSA \_ RedistributionControlRequired (0x08) 
    -    (COPP \_ CGMSA \_ REDISTRIBUTIONCONTROLREQUIRED + COPP \_ CGMSA \_ CopyNever) 或 COPP \_ CGMSA \_ LevelMax

<!-- -->

-   对于 COPP \_ ProtectionType \_ hdcp，请从 **COPP \_ HDCP \_ Protection \_ Level** 枚举类型设置以下值之一：
    -   COPP \_ hdcp \_ LEVEL0 或 COPP \_ hdcp \_ LevelMin (0) 
    -   COPP \_ hdcp \_ 一级或 COPP \_ HDCP \_ LevelMax (1) 

 

