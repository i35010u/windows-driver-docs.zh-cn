---
title: 智能卡读卡器的 WDM 设备名称
description: 智能卡读卡器的 WDM 设备名称
ms.assetid: 06f15b0d-d759-4cfe-a558-883f7f0d2581
keywords:
- 智能卡驱动程序 WDK、 设备名称
- 设备名称 WDK 智能卡
- 名称 WDK 智能卡
- 符号链接名称 WDK 智能卡
- 内核设备名称 WDK 智能卡
- WDM 设备名称 WDK 智能卡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d6ceba9efb6422a631671bb2e65b7b7d6788fa5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540379"
---
# <a name="wdm-device-names-for-smart-card-readers"></a>智能卡读卡器的 WDM 设备名称


## <span id="_ntovr_wdm_device_names_for_smart_card_readers"></span><span id="_NTOVR_WDM_DEVICE_NAMES_FOR_SMART_CARD_READERS"></span>


用于 WDM 设备驱动程序，内核设备名称是仅在内核在命名空间中已知的名称。 符号链接名称是 Microsoft Win32 应用程序使用与该驱动程序进行通信的名称。

由于仅在内核命名空间中的内核设备名称，驱动程序开发人员可以选择的名称，但它必须符合 Windows 操作系统中的设备名称的命名约定。 具体而言，设备名称必须如下所示：

*\\Device\\DeviceName\[Unit\]*

其中*DeviceName*是反映驱动程序的类型的名称和*单元*是该驱动程序的从零开始的单位数。 单位数用于区分一台设备文件系统中安装了该类型的多台设备时。

每个驱动程序必须与智能卡资源管理器进行通信，因为设备必须具有 Win32 命名空间中可访问的名称。 此符号链接名称必须如下所示：

*\\DosDevices\\SCReader\[Unit\]*

Win32 命名空间中的设备的单元号不必是用来构成的内核设备名称相同。 它应该是第一个可用的单元数。 使用[ **SmartcardCreateLink (WDM)** ](https://msdn.microsoft.com/library/windows/hardware/ff548935)自动生成符号链接的名称。

 

 





