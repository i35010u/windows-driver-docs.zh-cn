---
title: 从总线驱动程序调用 PoStartNextPowerIrp
description: 从总线驱动程序调用 PoStartNextPowerIrp
ms.assetid: 4e23ebe1-c939-48e1-82bf-cdb4980a5a7b
keywords:
- 总线驱动程序 WDK 电源管理
- power Irp WDK 内核 PoStartNextPowerIrp
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5bce8e498f0ec7ee3f7acf8faa8c39c0d3c7a1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385269"
---
# <a name="calling-postartnextpowerirp-from-a-bus-driver"></a>从总线驱动程序调用 PoStartNextPowerIrp





使用 Windows Vista 开始，调用[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)不是必需的和此例程的调用会执行任何电源管理操作。 但是，在 Windows Server 2003、 Windows XP 和 Windows 2000，总线驱动程序必须调用**PoStartNextPowerIrp**一次为每个[ **IRP\_MN\_查询\_电源** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)或[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)驱动程序收到的请求。

总线驱动程序始终调用该例程中其*DispatchPower*例程中，调用之前[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)例程。

 

 




