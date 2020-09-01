---
title: 处理总线驱动程序中的系统 Query-Power IRP
description: 处理总线驱动程序中的系统 Query-Power IRP
ms.assetid: d42c268e-d57d-41a6-8e61-67c651082106
keywords:
- 查询-power Irp WDK 电源管理
- 总线驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd8f4ce3ef709b2a68df51a20766e17ba52d498e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183859"
---
# <a name="handling-a-system-query-power-irp-in-a-bus-driver"></a>处理总线驱动程序中的系统 Query-Power IRP





当系统查询-电源请求到达不是设备) 的电源策略所有者 (的总线驱动程序时，驱动程序将确保它可以支持与查询的系统电源状态相对应的设备电源状态，并且如果启用了唤醒，则查询的系统电源状态不会阻止其设备唤醒系统。

在 Windows 7 和 Windows Vista 中，如果驱动程序可以更改为指定电源状态，则总线驱动程序将 **Irp- &gt; IoStatus** 设置为 \_ "成功"; 如果驱动程序无法使用，则将设置为 "失败" 状态。

在 Windows Server 2003、Windows XP 和 Windows 2000 中，总线驱动程序首先调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) ，然后将 **Irp- &gt; IoStatus** 设置为 \_ "成功"。如果驱动程序可以更改为指定电源状态，则为 "成功"; 如果驱动程序无法，则将设置为 "失败" 状态。

在总线驱动程序完成 IRP 后，电源管理器将调用由其他驱动程序设置的 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，因为它们向下传递 IRP。

 

