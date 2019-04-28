---
title: 对供应商提供的 IDE 控制器微型驱动程序的要求
description: 对供应商提供的 IDE 控制器微型驱动程序的要求
ms.assetid: a1584665-8788-49a4-b86f-50c265e7ce7a
keywords:
- IDE 控制器微型驱动程序 WDK 存储，供应商提供
- 存储 IDE 控制器微型驱动程序 WDK，供应商提供
- 供应商提供 IDE 控制器微型驱动程序 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c6db1bc511f5dc21e4d8e6c3ccd7ef3a1c3a568
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352627"
---
# <a name="requirements-for-vendor-supplied-ide-controller-minidrivers"></a>对供应商提供的 IDE 控制器微型驱动程序的要求


## <span id="ddk_requirements_for_vendor_supplied_ide_controller_minidrivers_kg"></span><span id="DDK_REQUIREMENTS_FOR_VENDOR_SUPPLIED_IDE_CONTROLLER_MINIDRIVERS_KG"></span>


本部分介绍 Microsoft Windows 要求的供应商提供 IDE 控制器微型驱动程序。

Microsoft 提供 IDE 端口驱动程序， *atapi.sys*，和控制器驱动程序*pciidex.sys*、 是独立于硬件的和可用于几乎所有 IDE 控制器。 因此，供应商提供端口驱动程序和控制器驱动程序不需要。

Microsoft 还提供了本机控制器微型驱动程序， *pciide.sys*、 用于处理控制器驱动程序微型驱动程序对依赖于硬件的方面和可用于大多数 IDE 控制器硬件。 供应商可以选择提供他们自己控制器微型驱动程序而不是使用*pciide.sys*。

供应商提供的控制器微型驱动程序不需要以支持插即用 (PnP) 或电源管理。 PnP 和电源管理操作由 Microsoft 提供的控制器的驱动程序，处理*pciidex.sys*。

供应商提供的控制器微型驱动程序不需要注册任何特定的接口，以符合系统要求。

供应商提供的控制器微型驱动程序不应尝试访问注册表，也不应调用内核模式之外 PciIdeX 库提供的例程。

供应商提供的控制器微型驱动程序必须提供一的组标准的微型驱动程序例程，它允许系统提供的控制器驱动程序以透明方式执行依赖于硬件的操作。

有关 PciIdeX 库和系统提供的控制器驱动程序和供应商提供的控制器微型驱动程序之间的微型驱动程序例程接口的说明的详细信息，请参阅[正在初始化和调用 IDE 微型驱动程序例程](initializing-and-calling-ide-minidriver-routines.md)。

 

 




