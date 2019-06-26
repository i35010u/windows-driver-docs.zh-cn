---
title: 处理总线驱动程序中的系统 Query-Power IRP
description: 处理总线驱动程序中的系统 Query-Power IRP
ms.assetid: d42c268e-d57d-41a6-8e61-67c651082106
keywords:
- 查询能耗 Irp WDK 电源管理
- 总线驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5bb2b5d1e0e5f91dc8ffd00fd62aab0ef7f890d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384247"
---
# <a name="handling-a-system-query-power-irp-in-a-bus-driver"></a>处理总线驱动程序中的系统 Query-Power IRP





当系统查询能耗请求到达总线驱动程序 （这不是设备的电源策略所有者） 时，驱动程序将确保它可以支持对应于查询的系统电源状态的设备电源状态，如果启用了唤醒，该查询的系统电源状态不会阻止其设备唤醒系统。

在 Windows 7 和 Windows Vista，总线驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功如果驱动程序可以将更改为指定的电源状态，或如果驱动程序不能设置的故障状态。

在 Windows Server 2003、 Windows XP 和 Windows 2000 中，总线驱动程序首先调用[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp) ，然后设置**Irp-&gt;IoStatus.Status**到状态\_成功如果驱动程序可以将更改为指定的电源状态，或如果驱动程序不能设置失败状态。

电源管理器 IRP 总线驱动程序之后，调用[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程由其他驱动程序设置，为他们通过 IRP 向下堆栈。

 

 




