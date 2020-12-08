---
title: 从总线驱动程序调用 PoStartNextPowerIrp
description: 从总线驱动程序调用 PoStartNextPowerIrp
keywords:
- 总线驱动程序 WDK 电源管理
- power Irp WDK 内核，PoStartNextPowerIrp
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: af0e368a121997141ab3b6e29f304929dd82a795
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816149"
---
# <a name="calling-postartnextpowerirp-from-a-bus-driver"></a>从总线驱动程序调用 PoStartNextPowerIrp





从 Windows Vista 开始，调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 不是必需的，并且调用此例程不会执行任何电源管理操作。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，总线驱动程序必须针对每个 [**IRP \_ MN \_ 查询 \_ 能力**](./irp-mn-query-power.md)或 [**irp \_ MN \_ 设置 \_**](./irp-mn-set-power.md)驱动程序收到的 power request 调用 **PoStartNextPowerIrp** 一次。

在调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)例程之前，总线驱动程序始终在其 *DispatchPower* 例程中调用此例程。

 

