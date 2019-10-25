---
title: 访问 PCI 配置空间
description: 访问 PCI 配置空间
ms.assetid: 4ec520db-7976-40e8-8336-f9056dc024b1
keywords:
- PCI 配置空间 WDK 音频
- 音频适配器驱动程序 WDK，PCI 配置空间
- 适配器驱动程序 WDK 音频，PCI 配置空间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7225db48bdd93155e777fe927822b314a331ada4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831410"
---
# <a name="accessing-pci-configuration-space"></a>访问 PCI 配置空间


## <span id="accessing_pci_configuration_space"></span><span id="ACCESSING_PCI_CONFIGURATION_SPACE"></span>


在 Windows Me/98 和 Windows 2000 及更高版本中，适配器驱动程序可以通过使用[**IRP\_MN\_读取\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)和[**IRP\_MN\_写入来访问其适配器卡的 PCI 配置空间，以 IRQL 被动\_级别。__t_10_ CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)请求。

在 Windows 2000 和更高版本中，PCI 驱动程序堆栈会将[**总线\_接口导出\_标准**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)接口，该接口提供对位于 IRQL 调度\_级别的 PCI 配置空间的访问。

有关详细信息，请参阅[访问设备配置空间](https://docs.microsoft.com/windows-hardware/drivers/kernel/accessing-device-configuration-space)。

 

 




