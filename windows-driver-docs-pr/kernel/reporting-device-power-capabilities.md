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
- I/O 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f87b33f36ad1518e2b5d320a43bbe6016f551b91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324495"
---
# <a name="reporting-device-power-capabilities"></a>报告设备电源功能





在枚举驱动程序报告特定于设备的信息以响应即插即用[ **IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)请求。 驱动程序以及其他此类信息，报告中的设备的电源管理功能[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构。 通常情况下，总线驱动程序将填充此结构。

更高级别的驱动程序应设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程的查询功能 IRP，以便它们可以创建结构的本地副本，并确保其包含适当的值。 作为一般规则，更高级别的驱动程序不应更改这些值。 但是，如果更改是必需的则驱动程序可以进一步限制设备功能，但不能向其中添加。 换而言之，驱动程序可以使限制性更强的规则，但不能放宽它们。

IRP 完成且已运行所有驱动程序完成例程后，缓存该结构和驱动程序不能更改其内容。

以下成员**设备\_功能**与电源管理相关的结构：

[DeviceD1 和 DeviceD2](deviced1-and-deviced2.md)

[WakeFromD0、 WakeFromD1、 WakeFromD2 和 WakeFromD3](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)

[DeviceState](devicestate.md)

[SystemWake](systemwake.md)

[DeviceWake](devicewake.md)

[D1Latency、 D2Latency 和 D3Latency](d1latency--d2latency--and-d3latency.md)

 

 




