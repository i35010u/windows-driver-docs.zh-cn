---
title: 编写 Unload 例程
description: 编写 Unload 例程
ms.assetid: 578f3499-28fc-412b-bbb7-75f8023fa7c1
keywords:
- 标准驱动程序例程 WDK 内核，卸载例程
- 驱动程序例程 WDK 内核，卸载例程
- 例程 WDK 内核，卸载例程
- 卸载例程的 WDK 内核
- 卸载例程 WDK 内核，关于卸载例程
- 替换驱动程序
- 驱动程序替换 WDK 内核
- 卸载驱动程序
- 重新加载驱动程序 WDK 内核
- 卸载 WDK 内核的驱动程序
- 重新加载 WDK 内核的驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc05fad7f57bf8dda46eed8aad5bb968a857562f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184943"
---
# <a name="writing-an-unload-routine"></a>编写 Unload 例程





当系统运行时，任何可以替换、卸载和重新加载的驱动程序都必须具有 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程。 所有 WDM 驱动程序必须具有 *卸载* 例程。

尽管 *卸载* 例程对于非 WDM 驱动程序是可选的，但 [驱动程序验证](../devtest/driver-verifier.md) 器将无法提供 *卸载* 例程的任何驱动程序。

本节包含下列主题：

[Unload 例程环境](unload-routine-environment.md)

[Unload 例程的功能](unload-routine-functionality.md)

 

