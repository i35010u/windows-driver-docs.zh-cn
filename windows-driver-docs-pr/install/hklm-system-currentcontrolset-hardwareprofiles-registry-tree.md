---
title: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles 注册表树
description: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles 注册表树包含有关系统上的硬件配置文件的信息。
ms.assetid: 548d7a50-b3b1-4413-8898-9ed13bcbdcfc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 503f03884b3b41dee026d560a1f8067fe4491097
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095281"
---
# <a name="hklmsystemcurrentcontrolsethardwareprofiles-registry-tree"></a>HKLM \\ SYSTEM \\ CurrentControlSet \\ HardwareProfiles 注册表树





**HKLM \\ system \\ CurrentControlSet \\ HardwareProfiles**注册表树包含有关系统上的硬件配置文件的信息。 不推荐使用硬件配置文件，且不应相对于硬件配置文件存储状态。

而是使用 **PLUGPLAY_REGKEY_DEVICE** 和 **PLUGPLAY_REGKEY_DRIVER** 全局存储信息，而无需使用 **PLUGPLAY_REGKEY_CURRENT_HWPROFILE**。 有关详细信息，请参阅 [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)。