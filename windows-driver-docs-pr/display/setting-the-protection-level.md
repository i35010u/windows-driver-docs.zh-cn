---
title: 设置保护级别
description: 设置保护级别
ms.assetid: e0fecc58-59d9-470a-83e6-9b08e2f59169
keywords:
- 复制保护 WDK COPP，保护级别
- 视频副本保护 WDK COPP，保护级别
- COPP WDK DirectX VA，保护级别
- 受保护的视频 WDK COPP，保护级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc8ac297866e20b52b2e3b63f3ff610954e31ce2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825809"
---
# <a name="setting-the-protection-level"></a>设置保护级别


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

COPP 命令可以设置与 DirectX VA COPP 设备关联的物理连接器上保护类型的保护级别。 若要设置保护级别，视频微型端口驱动程序的[*COPPCommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数接收指向[**DXVA\_COPPCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand)结构的指针，并将**guidCommandID**成员设置为 DXVA\_COPPSetProtectionLevel GUID 和**CommandData**成员设置为指向[**DXVA\_COPPSetProtectionLevelCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsetprotectionlevelcmddata)结构的指针，该结构指定要设置的保护类型以及设置保护的级别。 如果保护级别不可用于保护类型，则 COPP 命令会将保护级别设置为 COPP\_NoProtectionLevelAvailable （-1）。 COPP 命令还可以在 DXVA\_COPPSetProtectionLevelCmdData 的**ExtendedInfoChangeMask**和**ExtendedInfoData**成员中指定某些扩展信息，以便为保护类型设置该视频微型端口驱动程序。

对于指定的保护类型，可以设置以下保护级别：

-   对于 COPP\_ProtectionType\_ACP，请从**COPP\_ACP\_保护\_级别**枚举类型设置以下值之一：
    -   COPP\_ACP\_Level0 或 COPP\_ACP\_LevelMin （0）
    -   COPP\_ACP\_级级别（1）
    -   COPP\_ACP\_级别2（2）
    -   COPP\_ACP\_3 级或 COPP\_ACP\_LevelMax （3）

<!-- -->

-   对于 COPP\_ProtectionType\_CGMSA，请从**COPP\_CGMSA\_保护\_级别**枚举类型设置以下值之一：
    -   COPP\_CGMSA\_Disabled 或 COPP\_CGMSA\_LevelMin （0）
    -   COPP\_CGMSA\_CopyFreely （1）
    -   COPP\_CGMSA\_CopyNoMore （2）
    -   COPP\_CGMSA\_CopyOneGeneration （3）
    -   COPP\_CGMSA\_CopyNever （4）
    -   COPP\_CGMSA\_RedistributionControlRequired （0x08）
    -   （COPP\_CGMSA\_RedistributionControlRequired + COPP\_CGMSA\_CopyNever）或 COPP\_CGMSA\_LevelMax

<!-- -->

-   对于 COPP\_ProtectionType\_HDCP，请设置以下值之一： **COPP\_HDCP\_保护\_级别**枚举类型：
    -   COPP\_HDCP\_Level0 或 COPP\_HDCP\_LevelMin （0）
    -   COPP\_HDCP\_级别1或 COPP\_HDCP\_LevelMax （1）

 

 





