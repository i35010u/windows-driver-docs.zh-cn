---
title: 执行特定于设备的空闲检测
description: 执行特定于设备的空闲检测
ms.assetid: 1a4e3b66-f1dc-4dc8-af8b-ed8138270c3c
keywords:
- 空闲检测 WDK 电源管理
- 设备特定的空闲检测 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18bc07b0b3f6cecfd7a227b7ba5e6697c5cac11a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187056"
---
# <a name="performing-device-specific-idle-detection"></a>执行特定于设备的空闲检测





根据特定于设备的条件，驱动程序可以执行其自己的空闲检测，而不是使用 power manager 的空闲检测例程。

此类驱动程序应将其空闲设备置于对当前系统电源状态有效的最小睡眠状态。 为此，驱动程序将请求 power IRP ([**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)) ，并使用次要 Irp 代码 [**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md)，并指定设备应转换为的设备电源状态。

 

