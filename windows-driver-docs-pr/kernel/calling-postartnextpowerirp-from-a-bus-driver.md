---
title: 从总线驱动程序调用 PoStartNextPowerIrp
description: 从总线驱动程序调用 PoStartNextPowerIrp
ms.assetid: 4e23ebe1-c939-48e1-82bf-cdb4980a5a7b
keywords:
- 总线驱动程序 WDK 电源管理
- power Irp WDK 内核，PoStartNextPowerIrp
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22ae5fd43ab86c566d6cda8dbdf7c97aeb19e412
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837163"
---
# <a name="calling-postartnextpowerirp-from-a-bus-driver"></a>从总线驱动程序调用 PoStartNextPowerIrp





从 Windows Vista 开始，调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)不是必需的，并且调用此例程不会执行任何电源管理操作。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，总线驱动程序**必须对每**个[**IRP\_MN\_QUERY\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power) or [**IRP\_MN\_设置\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) request驱动程序接收。

在调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)例程之前，总线驱动程序始终在其*DispatchPower*例程中调用此例程。

 

 




