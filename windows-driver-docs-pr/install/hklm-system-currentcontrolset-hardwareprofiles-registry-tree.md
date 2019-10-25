---
title: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles 注册表树
description: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles 注册表树包含有关系统上的硬件配置文件的信息。
ms.assetid: 548d7a50-b3b1-4413-8898-9ed13bcbdcfc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 796544177efe8d764f11f66418d97369cba725fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828809"
---
# <a name="hklmsystemcurrentcontrolsethardwareprofiles-registry-tree"></a>HKLM\\SYSTEM\\CurrentControlSet\\HardwareProfiles 注册表树





**HKLM\\system\\CurrentControlSet\\HardwareProfiles**注册表树包含有关系统上的硬件配置文件的信息。 不推荐使用硬件配置文件，且不应相对于硬件配置文件存储状态。

而是使用**PLUGPLAY_REGKEY_DEVICE**和**PLUGPLAY_REGKEY_DRIVER**全局存储信息，而无需使用**PLUGPLAY_REGKEY_CURRENT_HWPROFILE**。 有关详细信息，请参阅[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)。




