---
title: 处理总线驱动程序中的系统 Query-Power IRP
description: 处理总线驱动程序中的系统 Query-Power IRP
ms.assetid: d42c268e-d57d-41a6-8e61-67c651082106
keywords:
- 查询-power Irp WDK 电源管理
- 总线驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f03933e8352496b638d8cf612bf4b11f0be7f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836631"
---
# <a name="handling-a-system-query-power-irp-in-a-bus-driver"></a>处理总线驱动程序中的系统 Query-Power IRP





当系统查询-电源请求到达总线驱动程序（这不是设备的电源策略所有者）时，驱动程序将确保它可以支持与查询的系统电源状态相对应的设备电源状态，并且如果启用了唤醒，则查询的系统电源状态不会阻止设备唤醒系统。

在 Windows 7 和 Windows Vista 中，如果驱动程序可以更改为指定电源状态，则总线驱动程序将**Irp&gt;** 的状态设置为 "\_状态"，如果驱动程序无法更改，则设置为 "失败" 状态。

在 Windows Server 2003、Windows XP 和 Windows 2000 中，bus 驱动程序首先调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) ，然后将**Irp&gt;IoStatus**状态设置\_为 "成功" （如果驱动程序可以更改为指定电源状态或设置故障）如果驱动程序不能。

在总线驱动程序完成 IRP 后，电源管理器将调用由其他驱动程序设置的[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，因为它们向下传递 IRP。

 

 




