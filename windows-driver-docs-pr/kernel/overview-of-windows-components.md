---
title: Windows 组件概述
description: Windows 组件概述
keywords:
- Windows 组件 WDK
- Windows NT 组件 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 95ee3b91eb38e7ab5b3de77b0bb27d4a9a872f62
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091122"
---
# <a name="overview-of-windows-components"></a>Windows 组件概述





下图显示了 Windows 操作系统的主要内部组件。

![概括说明 Windows 组件的关系图](images/ntarch.png)

如图所示，Windows 操作系统包含用户模式组件和内核模式组件。 有关 Windows 用户模式和内核模式的详细信息，请参阅[用户模式和内核模式](../gettingstarted/user-mode-and-kernel-mode.md)。

驱动程序调用由各种内核组件导出的例程。 例如，若要创建设备对象，需调用由 I/O 管理器导出的 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 例程。 有关驱动程序可调用的内核模式例程的列表，请参阅“驱动程序支持例程”。

此外，驱动程序必须对来自操作系统的特定调用做出响应，并可对其他系统调用做出响应。 有关驱动程序可能需要支持的内核模式例程的列表，请参阅[标准驱动程序例程](./introduction-to-standard-driver-routines.md)。

并非所有内核模式组件都在上图中绘出。 有关内核模式组件的列表，请参阅[内核模式管理器和库](windows-kernel-mode-object-manager.md)。

 

