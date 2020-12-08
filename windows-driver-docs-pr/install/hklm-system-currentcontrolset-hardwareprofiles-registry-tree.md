---
title: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles 注册表树
description: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles 注册表树包含有关系统上的硬件配置文件的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f376d74b93e2226ca5904b28b552b2cd6b9ab694
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791743"
---
# <a name="hklmsystemcurrentcontrolsethardwareprofiles-registry-tree"></a>HKLM \\ SYSTEM \\ CurrentControlSet \\ HardwareProfiles 注册表树





**HKLM \\ system \\ CurrentControlSet \\ HardwareProfiles** 注册表树包含有关系统上的硬件配置文件的信息。 不推荐使用硬件配置文件，且不应相对于硬件配置文件存储状态。

而是使用 **PLUGPLAY_REGKEY_DEVICE** 和 **PLUGPLAY_REGKEY_DRIVER** 全局存储信息，而无需使用 **PLUGPLAY_REGKEY_CURRENT_HWPROFILE**。 有关详细信息，请参阅 [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)。
