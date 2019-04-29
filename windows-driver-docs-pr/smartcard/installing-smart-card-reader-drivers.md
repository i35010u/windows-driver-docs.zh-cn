---
title: 安装智能卡读卡器驱动程序
description: 安装智能卡读卡器驱动程序
ms.assetid: 6e641718-d6d0-4f09-8935-6b381ad0c085
keywords:
- 智能卡驱动程序 WDK，安装
- 供应商提供的驱动程序 WDK 智能卡，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e7ac7a11bca8f6712e4ffcdd872c30beace569d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354759"
---
# <a name="installing-smart-card-reader-drivers"></a>安装智能卡读卡器驱动程序


## <span id="_ntovr_installing_smart_card_reader_drivers"></span><span id="_NTOVR_INSTALLING_SMART_CARD_READER_DRIVERS"></span>


本部分提供特定于 Microsoft Windows 2000 和更高版本的操作系统的智能卡读卡器驱动程序的安装信息。

提供其自己的读卡器驱动程序的供应商应使每个驱动程序的成员**SmartCardReader**安装程序中的类[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)的驱动程序的 INF 文件。 供应商还必须添加一个部分，若要正确配置的智能卡服务。 例如：

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

提供其自己 UMDF 读卡器驱动程序的供应商需要注册表设置，以允许上部的 UMDF reflector 即插即用的筛选器驱动程序。 具体而言，在驱动程序 INF 文件中，此项时，需要：

```cpp
[Install.NT.Wdf]
UmdfKernelModeClientPolicy=AllowKernelModeClients
```

没有与安装智能卡读卡器驱动程序相关联的其他任何特殊要求。

有关在 Windows 2000 和更高版本的操作系统的设备安装的常规信息，请参阅[设备安装概述](https://msdn.microsoft.com/library/windows/hardware/ff549455)。









