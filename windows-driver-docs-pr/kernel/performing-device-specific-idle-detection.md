---
title: 执行特定于设备的空闲检测
description: 执行特定于设备的空闲检测
ms.assetid: 1a4e3b66-f1dc-4dc8-af8b-ed8138270c3c
keywords:
- 空闲检测 WDK 电源管理
- 特定于设备的空闲检测 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6f1784492aba54d97286929ee7c39a4236afccb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384742"
---
# <a name="performing-device-specific-idle-detection"></a>执行特定于设备的空闲检测





而不是使用电源管理器的空闲检测例程，驱动程序可以执行特定于设备的条件的其自己空闲检测。

这样的驱动程序应将其空闲设备放在有效的当前系统电源状态的最低可能睡眠状态中。 若要执行此操作，该驱动程序请求 power IRP ([**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp))，次要 IRP 代码[ **IRP\_MN\_设置\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)，指定设备应转换到的设备电源状态。

 

 




