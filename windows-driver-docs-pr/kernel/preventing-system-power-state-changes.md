---
title: 阻止系统电源状态更改
description: 阻止系统电源状态更改
keywords:
- 系统电源状态 WDK 内核，阻止更改
- 状态转换 WDK 电源管理
- PoRegisterSystemState
- PoSetSystemState
- PoUnregisterSystemState
- 工作状态 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c254c20a3cea78331d9ab4ec0fbdcbc78f559a18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783861"
---
# <a name="preventing-system-power-state-changes"></a>阻止系统电源状态更改





尽管驱动程序不能直接设置系统电源策略，但电源管理器提供了三个例程，驱动程序可通过这些例程防止系统转换出工作状态： [**PoSetSystemState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemstate)、 [**PoRegisterSystemState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregistersystemstate)和 [**PoUnregisterSystemState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pounregistersystemstate)。

通过调用 **PoRegisterSystemState** 或 **PoSetSystemState**，驱动程序可以通知电源管理器用户存在，或者驱动程序需要使用系统或显示。

**PoRegisterSystemState** 允许驱动程序注册连续繁忙状态。 它将返回一个句柄，驱动程序可在以后更改其设置。 只要状态注册生效，电源管理器不会尝试将系统置于睡眠状态。 驱动程序通过调用 **PoUnregisterSystemState** 取消状态注册。

使用 **PoSetSystemState** 时，驱动程序会在 (用户、需要系统、显示所需的) 的情况下通知电源管理器，但此设置不是连续的。 它具有重新启动任何与指定条件关联的空闲计数的影响。

使用这些例程，驱动程序可以 forestall 多个（但不是全部）从工作状态进行的转换。 当掉电断电或用户显式请求关闭时，电源管理器始终关闭系统。

 

