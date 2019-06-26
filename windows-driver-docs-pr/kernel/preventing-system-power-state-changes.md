---
title: 阻止系统电源状态更改
description: 阻止系统电源状态更改
ms.assetid: a744dfe7-d756-45c3-8fdf-7a403f6cde36
keywords:
- 系统电源状态 WDK 内核，阻止更改
- 状态转换 WDK 电源管理
- PoRegisterSystemState
- PoSetSystemState
- PoUnregisterSystemState
- 工作状态 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76fc89283d06eae980b2e7238b80c99246b078c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378828"
---
# <a name="preventing-system-power-state-changes"></a>阻止系统电源状态更改





虽然驱动程序不能直接设置系统电源策略，但电源管理器提供了三个例程，通过该驱动程序可以阻止从工作状态的系统转换：[**PoSetSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-posetsystemstate)， [ **PoRegisterSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-poregistersystemstate)，以及[ **PoUnregisterSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pounregistersystemstate)。

通过调用**PoRegisterSystemState**或**PoSetSystemState**，驱动程序可以通知电源管理器，用户是否存在或该驱动程序需要使用的系统或显示。

**PoRegisterSystemState**使驱动程序以注册连续的忙碌状态。 它将返回的句柄，通过该驱动程序可以在以后更改其设置。 只要状态注册生效时，电源管理器不会尝试将系统进入睡眠状态。 该驱动程序通过调用取消状态注册**PoUnregisterSystemState**。

与**PoSetSystemState**、 驱动程序会通知相同的条件 （存在用户，所需的系统，显示所需） 的电源管理器，但此设置不连续。 它具有重启与指定的条件相关联的任何空闲计数列表的效果。

使用这些例程，驱动程序可以阻止许多，但并非所有转换从工作状态。 电源管理器始终关闭系统即将断电时或者当用户显式请求关闭。

 

 




