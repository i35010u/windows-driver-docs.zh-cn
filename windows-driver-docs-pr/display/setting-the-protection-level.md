---
title: 设置保护级别
description: 设置保护级别
ms.assetid: e0fecc58-59d9-470a-83e6-9b08e2f59169
keywords:
- 复制保护 WDK COPP，保护级别
- 视频复制保护 WDK COPP，保护级别
- COPP WDK DirectX VA，保护级别
- 受保护视频 WDK COPP，保护级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14a824c65fa68b8a90d7547b3ca7901c191580ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383859"
---
# <a name="setting-the-protection-level"></a>设置保护级别


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

COPP 命令可以在与 DirectX VA COPP 设备相关联的物理连接器上设置保护类型的保护级别。 若要设置的保护级别，微型端口驱动程序的[ *COPPCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff539642)函数接收指向[ **DXVA\_COPPCommand**](https://msdn.microsoft.com/library/windows/hardware/ff563141)结构**guidCommandID**成员设置为 DXVA\_COPPSetProtectionLevel GUID 并**CommandData**成员设置为指向[ **DXVA\_COPPSetProtectionLevelCmdData** ](https://msdn.microsoft.com/library/windows/hardware/ff563143)结构，它指定到保护组和要设置的保护级别的类型。 如果保护级别不适用于保护类型，COPP 命令将保护级别设置为 COPP\_NoProtectionLevelAvailable (-1)。 COPP 命令还可能指定中的一些扩展的信息**ExtendedInfoChangeMask**并**ExtendedInfoData** DXVA 成员\_COPPSetProtectionLevelCmdData 视频若要为保护类型设置的微型端口驱动程序。

可以为所指示的保护类型设置以下保护级别：

-   有关 COPP\_ProtectionType\_ACP，设置中的以下值之一**COPP\_ACP\_保护\_级别**枚举类型：
    -   COPP\_ACP\_级别 0 或 COPP\_ACP\_LevelMin (0)
    -   COPP\_ACP\_级别 1 (1)
    -   COPP\_ACP\_Level2 (2)
    -   COPP\_ACP\_Level3 或 COPP\_ACP\_LevelMax (3)

<!-- -->

-   有关 COPP\_ProtectionType\_CGMSA，设置中的以下值之一**COPP\_CGMSA\_保护\_级别**枚举类型：
    -   COPP\_CGMSA\_禁用或 COPP\_CGMSA\_LevelMin (0)
    -   COPP\_CGMSA\_CopyFreely (1)
    -   COPP\_CGMSA\_CopyNoMore (2)
    -   COPP\_CGMSA\_CopyOneGeneration (3)
    -   COPP\_CGMSA\_CopyNever (4)
    -   COPP\_CGMSA\_RedistributionControlRequired (0x08)
    -   (COPP\_CGMSA\_RedistributionControlRequired + COPP\_CGMSA\_CopyNever) 或 COPP\_CGMSA\_LevelMax

<!-- -->

-   有关 COPP\_ProtectionType\_HDCP，设置中的以下值之一**COPP\_HDCP\_保护\_级别**枚举类型：
    -   COPP\_HDCP\_级别 0 或 COPP\_HDCP\_LevelMin (0)
    -   COPP\_HDCP\_Level1 或 COPP\_HDCP\_LevelMax (1)

 

 





