---
title: 智能卡读卡器的 WDM 设备名称
description: 智能卡读卡器的 WDM 设备名称
ms.assetid: 06f15b0d-d759-4cfe-a558-883f7f0d2581
keywords:
- 智能卡驱动程序 WDK，设备名称
- 设备名称 WDK 智能卡
- 命名 WDK 智能卡
- 符号链接名称 WDK 智能卡
- 内核设备名称 WDK 智能卡
- WDM 设备名称 WDK 智能卡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d614f9f0ffe2899ee1c0cbdac017f7c5feb2f9a9
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382561"
---
# <a name="wdm-device-names-for-smart-card-readers"></a>智能卡读卡器的 WDM 设备名称


## <span id="_ntovr_wdm_device_names_for_smart_card_readers"></span><span id="_NTOVR_WDM_DEVICE_NAMES_FOR_SMART_CARD_READERS"></span>


对于 WDM 设备驱动程序，内核设备名称只是在内核的名称空间中已知的名称。 符号链接名称是 Microsoft Win32 应用程序用来与驱动程序通信的名称。

因为内核设备名称只在内核命名空间中知道，驱动程序开发人员可以选择名称，但必须符合 Windows 操作系统中设备名称的命名约定。 具体而言，设备名称必须如下所示：

*\\设备 \\ DeviceName \[ 单位\]*

其中， *DeviceName* 是反映驱动程序类型的名称， *单位* 是该驱动程序的从零开始的单位号。 如果系统中安装了多个设备，则使用单位号来区分一台设备。

由于每个驱动程序必须与智能卡资源管理器通信，因此设备必须具有可在 Win32 命名空间中访问的名称。 此符号链接名称必须如下所示：

*\\DosDevices \\ SCReader \[ 单元\]*

Win32 命名空间中的设备的单位号不必与用于形成内核设备名称的设备号相同。 它应该是第一个可用的单位号。 使用 [**SmartcardCreateLink (WDM) **](/previous-versions/ff548935(v=vs.85)) 自动生成符号链接名称。

 

