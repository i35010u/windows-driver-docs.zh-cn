---
title: 支持多功能 PC 卡设备
description: 支持多功能 PC 卡设备
ms.assetid: 4da3b99c-0731-41b5-9f67-29c7e181342f
keywords:
- 多功能设备 WDK、 PC 卡
- PC 卡多功能标准 WDK
- 资源映射 WDK 多功能设备
- 16 位 PC 卡多功能设备 WDK
- 配置注册 WDK 多功能设备
- 注册 WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b33988d24ad7fd53dc3c620d7187a676a70ca1cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533719"
---
# <a name="supporting-multifunction-pc-card-devices"></a>支持多功能 PC 卡设备





PC 卡多功能标准指定多功能设备属性为在内存中的每个函数具有一组配置注册表。 这些寄存器允许 PCMCIA 总线驱动程序，例如，单独启用每个函数，并定义专用于每个函数的 I/O 资源。 标准还指定多功能设备包含，在属性内存中，每个集配置寄存器的地址。 这些地址启用 PCMCIA 总线驱动程序进行编程配置注册表。

如果 16 位 PC 卡设备完全实施 PC 卡多功能标准，并且正确，此类设备的供应商的最小的 INF 和驱动程序要求，以确保设备是在基于 NT 的系统上正确配置。 请参阅[支持 PC 卡，符合多功能标准](supporting-pc-cards-that-conform-to-the-multifunction-standard.md)有关详细信息。

如果 16 位 PC 卡设备未完全实现 PC 卡多功能标准，供应商必须提供 INF 文件中缺少的信息。 有两种方法的多功能 PC 卡设备可能无法实现多功能标准：

1.  设备实现一组的每个函数的多功能配置注册表，但不包含在其特性内存中的寄存器的所有集的位置。

2.  设备未实现每个函数的多功能配置注册表的设置。

如果设备具有上面列出的限制，如果该设备 INF 中包含所需的信息，PCMCIA 总线驱动程序可以编程配置寄存器*DDInstall*。**LogConfigOverride**稿件。 请参阅以下各节，有关详细信息：

[支持具有不完整的配置的 PC 卡注册地址](supporting-pc-cards-that-have-incomplete-configuration-register-addres.md)

[支持具有不完整的配置的 PC 卡注册](supporting-pc-cards-that-have-incomplete-configuration-registers.md)

Cardbus 设备实质上是遵循 PCI 多功能规则。 请参阅[支持多功能 PCI 设备](supporting-multifunction-pci-devices.md)。

 

 




