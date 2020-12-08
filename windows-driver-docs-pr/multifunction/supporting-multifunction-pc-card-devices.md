---
title: 支持多功能电脑卡设备
description: 支持多功能电脑卡设备
keywords:
- 多功能设备 WDK，PC 卡
- PC 卡多功能标准版 WDK
- 资源映射 WDK 多功能设备
- 16位 PC 卡多功能设备 WDK
- 配置注册 WDK 多功能设备
- 注册 WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf2381e29bf6bfb3e31ecd75f9a420e6ec6982bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827587"
---
# <a name="supporting-multifunction-pc-card-devices"></a>支持多功能电脑卡设备





PC 卡多功能标准版指定多功能设备在属性内存中为每个函数提供一组配置注册。 例如，这些寄存器允许 PCMCIA 总线驱动程序单独启用每个函数，并定义每个函数独占的一系列 i/o 资源。 标准还指定了多功能设备在属性内存中包含每组配置注册的地址。 这些地址使 PCMCIA 总线驱动程序可以对配置寄存器进行编程。

如果16位 PC 卡设备完全和正确地实现了 PC 卡多功能标准，则此类设备的供应商将具有最低的 INF 和驱动程序要求，以确保在基于 NT 的系统上正确配置设备。 有关详细信息，请参阅 [支持符合多功能标准的 PC 卡](supporting-pc-cards-that-conform-to-the-multifunction-standard.md) 。

如果16位 PC 卡设备未完全实现 PC 卡多功能标准版，则供应商必须在 INF 文件中提供缺少的信息。 多功能 PC 卡设备可能会通过两种方式实现多功能标准：

1.  设备为每个函数实现一组多功能配置寄存器，但不包含其属性内存中所有寄存器集的位置。

2.  设备不实现每个函数的一组多功能配置注册。

如果设备具有上面列出的限制，则当设备的 INF 在 *DDInstall* 中包含所需的信息时，PCMCIA 总线驱动程序可以对配置寄存器进行编程。**LogConfigOverride** 节 (s) 。 有关详细信息，请参阅以下部分：

[支持具有不完整配置寄存器地址的电脑卡](supporting-pc-cards-that-have-incomplete-configuration-register-addres.md)

[支持具有不完整配置寄存器的电脑卡](supporting-pc-cards-that-have-incomplete-configuration-registers.md)

Cardbus 设备实质上遵循 PCI 多功能规则。 请参阅 [支持多功能 PCI 设备](supporting-multifunction-pci-devices.md)。

 

 




