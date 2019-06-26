---
title: 电源管理器
description: 电源管理器
ms.assetid: f7727368-6edd-427b-9fb3-02f80538807b
keywords:
- 电源管理器 WDK 内核
- 使用情况 manager WDK 电源管理
- power Irp WDK 内核，电源管理器
- 整个系统电源策略 WDK 内核
- 电源策略 WDK 内核
- 睡眠电源管理 WDK 内核
- 休眠电源管理 WDK 内核
- 关闭电源管理 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8831d9c30c160b29283445174709ba90125e8869
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374194"
---
# <a name="power-manager"></a>电源管理器





电源管理器负责管理系统的电源使用情况。 它管理整个系统电源策略，并跟踪通过系统电源 Irp 的路径。

电源管理器请求通过发送电源操作[ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)对驱动程序的请求。 请求可以指定新的电源状态，或者可以查询电源状态更改不可行。

电源管理器需要睡眠、 休眠或关机时，通过将发送请求相应的电源操作**IRP\_MJ\_POWER**到设备树中每个叶节点的请求。 在确定是否在系统会无限地休眠，以下进入休眠状态，或关闭的情况下，会考虑电源管理器：

-   系统活动级别

-   系统电池电量水平

-   关闭、 进入休眠状态，或进入睡眠状态来自应用程序请求

-   用户操作，例如，按下电源按钮

-   控制面板设置

有关详细信息，请参阅[Windows 内核模式电源管理器](windows-kernel-mode-power-manager.md)。

 

 




