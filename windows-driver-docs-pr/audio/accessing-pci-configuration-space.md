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
ms.openlocfilehash: fe9c12271e1912c9238eea841aa2081ede59ccb8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208389"
---
# <a name="accessing-pci-configuration-space"></a>访问 PCI 配置空间


## <span id="accessing_pci_configuration_space"></span><span id="ACCESSING_PCI_CONFIGURATION_SPACE"></span>


在 Windows Me/98 和 Windows 2000 及更高版本中，适配器驱动程序可以 \_ 通过使用 [**irp \_ MN \_ READ \_ config**](../kernel/irp-mn-read-config.md) 和 [**irp \_ MN \_ 写入 \_ 配置**](../kernel/irp-mn-write-config.md) 请求来访问其适配器卡的 PCI 配置空间。

在 Windows 2000 和更高版本中，PCI 驱动程序堆栈导出 [**总线 \_ 接口 \_ 标准**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard) 接口，该接口提供对 IRQL 调度级别的 PCI 配置空间的访问 \_ 。

有关详细信息，请参阅 [访问设备配置空间](../kernel/accessing-device-configuration-space.md)。

 

