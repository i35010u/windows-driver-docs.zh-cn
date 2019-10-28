---
title: 执行特定于设备的空闲检测
description: 执行特定于设备的空闲检测
ms.assetid: 1a4e3b66-f1dc-4dc8-af8b-ed8138270c3c
keywords:
- 空闲检测 WDK 电源管理
- 设备特定的空闲检测 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c34f90a462cce823f4f7d6b1d90c05cd1a16253
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838510"
---
# <a name="performing-device-specific-idle-detection"></a>执行特定于设备的空闲检测





根据特定于设备的条件，驱动程序可以执行其自己的空闲检测，而不是使用 power manager 的空闲检测例程。

此类驱动程序应将其空闲设备置于对当前系统电源状态有效的最小睡眠状态。 为此，驱动程序将使用次要 IRP 代码 IRP 请求一个电源 IRP （[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)） [ **\_MN\_设置\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)，指定设备应转换为的设备电源状态。

 

 




