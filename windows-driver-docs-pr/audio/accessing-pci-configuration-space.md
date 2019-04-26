---
title: 访问 PCI 配置空间
description: 访问 PCI 配置空间
ms.assetid: 4ec520db-7976-40e8-8336-f9056dc024b1
keywords:
- PCI 配置空间 WDK 音频
- 音频适配器驱动程序 WDK、 PCI 配置空间
- 适配器驱动程序 WDK 音频，PCI 配置空间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b1ba8f3e1412004c97a482f65706019ad7ec9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327627"
---
# <a name="accessing-pci-configuration-space"></a>访问 PCI 配置空间


## <span id="accessing_pci_configuration_space"></span><span id="ACCESSING_PCI_CONFIGURATION_SPACE"></span>


在 Windows 中我 / 98，并且 Windows 2000 和更高版本，适配器驱动程序可以访问其适配器卡的 PCI 配置空间在 IRQL 被动\_级别通过使用[ **IRP\_MN\_读取\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)并[ **IRP\_MN\_编写\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551769)请求。

PCI 驱动程序在 Windows 2000 及更高版本，堆栈导出[**总线\_界面\_标准**](https://msdn.microsoft.com/library/windows/hardware/ff540707)接口，它提供了对在 IRQL 调度的 PCI 配置空间访问\_级别。

有关详细信息，请参阅[访问设备配置空间](https://msdn.microsoft.com/library/windows/hardware/ff540450)。

 

 




