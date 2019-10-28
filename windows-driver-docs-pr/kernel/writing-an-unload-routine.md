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
ms.openlocfilehash: 289c7ed0c67ac74329eb9db8fd20d182a979e5b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838290"
---
# <a name="writing-an-unload-routine"></a>编写 Unload 例程





当系统运行时，任何可以替换、卸载和重新加载的驱动程序都必须具有[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程。 所有 WDM 驱动程序必须具有*卸载*例程。

尽管*卸载*例程对于非 WDM 驱动程序是可选的，但[驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)器将无法提供*卸载*例程的任何驱动程序。

本部分包含以下主题：

[卸载例程环境](unload-routine-environment.md)

[卸载例程功能](unload-routine-functionality.md)

 

 




