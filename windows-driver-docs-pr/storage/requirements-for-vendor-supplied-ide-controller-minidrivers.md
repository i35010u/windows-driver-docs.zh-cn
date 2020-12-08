---
title: 供应商提供的 IDE 控制器微型驱动程序简介
description: 对供应商提供的 IDE 控制器微型驱动程序的要求
keywords:
- IDE 控制器微型驱动程序 WDK 存储，供应商提供
- 存储 IDE 控制器微型驱动程序 WDK，供应商提供
- 供应商提供的 IDE 控制器微型驱动程序 WDK 存储
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1addb796ceeb4923133c8555d6a278b64bce2e26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833277"
---
# <a name="introduction-to-vendor-supplied-ide-controller-minidrivers"></a>供应商提供的 IDE 控制器微型驱动程序简介

Microsoft 提供的 IDE 端口驱动程序、 *atapi.sys* 和控制器驱动程序 *pciidex.sys* 与硬件无关，并且几乎可与几乎所有 IDE 控制器一起使用。 因此，不需要供应商提供的端口驱动程序和控制器驱动程序。

Microsoft 还提供了本机控制器微型驱动程序， *pciide.sys*，它处理控制器驱动程序微型驱动程序对的硬件相关方面，并可用于大多数 IDE 控制器硬件。 供应商可以选择提供自己的控制器微型驱动程序，而不是使用 *pciide.sys*。

供应商提供的控制器微型驱动程序：

- 不需要支持即插即用 (PnP) 或电源管理。 PnP 和电源管理操作由 Microsoft 提供的控制器驱动程序（ *pciidex.sys*）处理。

- 无需注册任何特定接口即可符合系统要求。

- 不应尝试访问注册表或调用 *PciIdeX* 库提供的内核模式例程。

- 必须提供一组标准微型驱动程序例程，以允许系统提供的控制器驱动程序以透明方式执行与硬件相关的操作。

有关 *PciIdeX* 库的详细信息以及系统提供的控制器驱动程序与供应商提供的控制器微型驱动程序之间微型驱动程序例程接口的说明，请参阅 [初始化和调用 IDE 微型驱动程序例程](initializing-and-calling-ide-minidriver-routines.md)。

 

 




