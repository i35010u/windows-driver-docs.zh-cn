---
title: 电源管理器
description: 电源管理器
ms.assetid: f7727368-6edd-427b-9fb3-02f80538807b
keywords:
- power manager WDK 内核
- 使用情况管理器 WDK 电源管理
- power Irp WDK 内核，电源管理器
- 系统范围电源策略 WDK 内核
- 电源策略 WDK 内核
- 睡眠电源管理 WDK 内核
- 休眠电源管理 WDK 内核
- 关闭电源管理 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 358d949e02f2cd44391844e17aa4b838b4978aac
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184437"
---
# <a name="power-manager"></a>电源管理器





电源管理器负责管理系统的电源使用情况。 它管理系统范围的电源策略，并通过系统跟踪电源 Irp 的路径。

电源管理器通过将 [**IRP \_ MJ \_ 电源**](./irp-mj-power.md) 请求发送到驱动程序来请求电源操作。 请求可以指定新的电源状态，也可以查询电源状态的更改是否可行。

需要睡眠、休眠或关机时，电源管理器会通过将 **IRP \_ MJ \_ 电源** 请求发送到设备树中的每个叶节点来请求适当的电源操作。 在确定系统是睡眠、休眠还是关机时，电源管理器会考虑以下事项：

-   系统活动级别

-   系统电池电量水平

-   应用程序的关闭、休眠或睡眠请求

-   用户操作，如按下电源按钮

-   控制面板设置

有关详细信息，请参阅 [Windows 内核模式电源管理器](windows-kernel-mode-power-manager.md)。

 

