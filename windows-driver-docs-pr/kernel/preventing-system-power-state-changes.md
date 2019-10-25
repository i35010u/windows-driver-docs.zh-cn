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
ms.openlocfilehash: 3779d3bc717cbcb91c7befe5c75fe20c0c2c868f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827629"
---
# <a name="preventing-system-power-state-changes"></a>阻止系统电源状态更改





尽管驱动程序不能直接设置系统电源策略，但电源管理器提供了三个例程，驱动程序可通过这些例程防止系统转换出工作状态： [**PoSetSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemstate)、 [**PoRegisterSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregistersystemstate)和[**PoUnregisterSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pounregistersystemstate)。

通过调用**PoRegisterSystemState**或**PoSetSystemState**，驱动程序可以通知电源管理器用户存在，或者驱动程序需要使用系统或显示。

**PoRegisterSystemState**允许驱动程序注册连续繁忙状态。 它将返回一个句柄，驱动程序可在以后更改其设置。 只要状态注册生效，电源管理器不会尝试将系统置于睡眠状态。 驱动程序通过调用**PoUnregisterSystemState**取消状态注册。

使用**PoSetSystemState**时，驱动程序会向电源管理器通知相同的条件（用户存在、需要系统、显示），但此设置不是连续的。 它具有重新启动任何与指定条件关联的空闲计数的影响。

使用这些例程，驱动程序可以 forestall 多个（但不是全部）从工作状态进行的转换。 当掉电断电或用户显式请求关闭时，电源管理器始终关闭系统。

 

 




