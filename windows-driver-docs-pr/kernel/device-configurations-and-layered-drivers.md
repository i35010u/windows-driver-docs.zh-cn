---
title: 设备配置和分层驱动程序
description: 对于最常见的设备类型，Windows 驱动程序工具包 (WDK) 提供一组完整的功能系统驱动程序。
keywords:
- WDM 驱动程序 WDK 内核，配置
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 替换驱动程序
- 可重用的驱动程序 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2670181c3c1a73e677484944b256f92b248fe314
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805437"
---
# <a name="device-configurations-and-layered-drivers"></a>设备配置和分层驱动程序


对于最常见的设备类型，Windows 驱动程序工具包 (WDK) 提供一组完整的功能系统驱动程序。 为类似类型的设备开发新的驱动程序时，可以将单个示例驱动程序用作模型。 但是，系统的驱动程序具有额外的设计要求：以便于开发新的设备驱动程序。 因此，许多系统驱动程序都有一个分层体系结构，以便可以重用某些驱动程序来支持类似设备的新驱动程序。




在大多数情况下，WDK 提供的可重复使用的驱动程序为 WDM 驱动程序，支持 PnP，并为系统提供的特定于设备的最低级别 (PnP 总线) 驱动程序处理与硬件无关的操作。 在某些情况下（例如并行端口和 SCSI 端口驱动程序），这些可重用的驱动程序为更高级、特定于设备类型的类驱动程序提供支持。 请注意，系统的任何可重用驱动程序都不会阻止要添加到现有驱动程序链中的新中间驱动程序的开发。

在设备的驱动程序链中容纳新的 (或替换) 驱动程序的情况部分取决于给定 Windows 平台中设备的硬件配置，部分取决于现有系统驱动程序支持新驱动程序所需的数量。

## <a name="in-this-section"></a>在本节中


-   [示例设备和驱动程序配置](sample-device-and-driver-configuration.md)
-   [添加驱动程序时要考虑的要点](points-to-consider-when-adding-drivers.md)

 

 




