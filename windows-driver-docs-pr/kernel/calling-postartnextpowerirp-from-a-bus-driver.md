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
ms.openlocfilehash: 00906c9e5f99bb6d3c06e546593cb5d808641b54
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188647"
---
# <a name="calling-postartnextpowerirp-from-a-bus-driver"></a>从总线驱动程序调用 PoStartNextPowerIrp





从 Windows Vista 开始，调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 不是必需的，并且调用此例程不会执行任何电源管理操作。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，总线驱动程序必须针对每个[**IRP \_ MN \_ 查询 \_ 能力**](./irp-mn-query-power.md)或[**irp \_ MN \_ 设置 \_ **](./irp-mn-set-power.md)驱动程序收到的 power request 调用**PoStartNextPowerIrp**一次。

在调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)例程之前，总线驱动程序始终在其*DispatchPower*例程中调用此例程。

 

