---
title: 执行特定于设备的空闲检测
description: 执行特定于设备的空闲检测
keywords:
- 空闲检测 WDK 电源管理
- 设备特定的空闲检测 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90ff886be683ebacd9d7da53a5168fba0f4faf68
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839233"
---
# <a name="performing-device-specific-idle-detection"></a>执行特定于设备的空闲检测





根据特定于设备的条件，驱动程序可以执行其自己的空闲检测，而不是使用 power manager 的空闲检测例程。

此类驱动程序应将其空闲设备置于对当前系统电源状态有效的最小睡眠状态。 为此，驱动程序将请求 power IRP ([**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)) ，并使用次要 Irp 代码 [**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md)，并指定设备应转换为的设备电源状态。

 

