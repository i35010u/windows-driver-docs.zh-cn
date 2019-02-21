---
title: 执行特定于设备的空闲检测
description: 执行特定于设备的空闲检测
ms.assetid: 1a4e3b66-f1dc-4dc8-af8b-ed8138270c3c
keywords:
- 空闲检测 WDK 电源管理
- 特定于设备的空闲检测 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39749616b5348b6415eb2c6c7a52d13b693c0c64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534417"
---
# <a name="performing-device-specific-idle-detection"></a>执行特定于设备的空闲检测





而不是使用电源管理器的空闲检测例程，驱动程序可以执行特定于设备的条件的其自己空闲检测。

这样的驱动程序应将其空闲设备放在有效的当前系统电源状态的最低可能睡眠状态中。 若要执行此操作，该驱动程序请求 power IRP ([**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734))，次要 IRP 代码[ **IRP\_MN\_设置\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)，指定设备应转换到的设备电源状态。

 

 




