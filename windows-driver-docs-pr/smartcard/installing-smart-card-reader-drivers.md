---
title: 安装智能卡读卡器驱动程序
description: 安装智能卡读卡器驱动程序
ms.assetid: 6e641718-d6d0-4f09-8935-6b381ad0c085
keywords:
- 智能卡驱动程序 WDK，安装
- 供应商提供的驱动程序 WDK 智能卡，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02d45cd4015ba98bd00498866279fa8630c2acb0
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384001"
---
# <a name="installing-smart-card-reader-drivers"></a>安装智能卡读卡器驱动程序


## <span id="_ntovr_installing_smart_card_reader_drivers"></span><span id="_NTOVR_INSTALLING_SMART_CARD_READER_DRIVERS"></span>


本部分提供特定于 Microsoft Windows 的智能卡读卡器驱动程序的安装信息。

提供自己的读取器驱动程序的供应商应该使每个驱动程序成为驱动程序 INF 文件的 " [**Inf 版本" 部分**](../install/inf-version-section.md)中的**SmartCardReader**安装程序类的成员。 供应商还必须添加一个部分来正确配置智能卡服务。 例如：

```cpp
[Version]
Signature="$Windows NT$"
Class=SmartCardReader
ClassGuid={50DD5230-BA8A-11D1-BF5D-0000F805F530}

; ============ Add reg for all readers ===============

[Reader.Install.AddReg]
HKLM, Software\Microsoft\Cryptography\Calais\Readers,,,
HKLM, System\CurrentControlSet\Services\SCardSvr,Start,0x00010001,2
HKLM, System\CurrentControlSet\Services\CertPropSvc,Start,0x00010001,2
```

提供自己的 UMDF 读取器驱动程序的供应商需要一个注册表设置，以允许 PnP 筛选器驱动程序驻留在 UMDF 反射器的顶部。 具体而言，在驱动程序 INF 文件中，此项是必需的：

```cpp
[Install.NT.Wdf]
UmdfKernelModeClientPolicy=AllowKernelModeClients
```

不存在与安装智能卡读卡器驱动程序相关的其他特殊要求。

有关 Windows 中的设备安装的常规信息，请参阅 [设备安装概述](../install/overview-of-device-and-driver-installation.md)。