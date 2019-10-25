---
title: 报告设备电源功能
description: 报告设备电源功能
ms.assetid: 67a504d0-2c41-4c74-a912-4f0771885f7d
keywords:
- 报告设备电源功能
- 设备电源功能 WDK 内核
- DEVICE_CAPABILITIES 结构
- 查询功能 Irp WDK 电源管理
- Irp WDK 电源管理
- I/o 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a17e9f0d089d6c7c87e9b76cfc39a2164686c885
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838451"
---
# <a name="reporting-device-power-capabilities"></a>报告设备电源功能





枚举过程中，驱动程序会报告设备特定的信息，以响应 PnP [**IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求。 除了其他此类信息，驱动程序还会在[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中报告设备的电源管理功能。 通常，总线驱动程序会填充此结构。

较高级别的驱动程序应为查询功能 IRP 设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，使其可以创建结构的本地副本，并确保其包含适当的值。 作为一般规则，较高级别的驱动程序不应更改这些值。 但是，如果需要进行更改，则驱动程序可以进一步限制设备功能，但无法添加设备功能。 换句话说，驱动程序可以使规则具有更强的限制，但不能将它们放宽。

完成 IRP 并运行所有驱动程序的完成例程后，将缓存该结构，并且驱动程序无法更改其内容。

设备的以下成员 **\_功能**结构与电源管理相关：

[DeviceD1 和 DeviceD2](deviced1-and-deviced2.md)

[WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)

[DeviceState](devicestate.md)

[SystemWake](systemwake.md)

[DeviceWake](devicewake.md)

[D1Latency、D2Latency 和 D3Latency](d1latency--d2latency--and-d3latency.md)

 

 




