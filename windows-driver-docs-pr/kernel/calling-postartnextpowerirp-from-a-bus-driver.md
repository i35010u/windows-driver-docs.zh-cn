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
ms.openlocfilehash: 337eb2b92772d5da8513dce6a16c4e14afff047d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338610"
---
# <a name="calling-postartnextpowerirp-from-a-bus-driver"></a>从总线驱动程序调用 PoStartNextPowerIrp





使用 Windows Vista 开始，调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)不是必需的和此例程的调用会执行任何电源管理操作。 但是，在 Windows Server 2003、 Windows XP 和 Windows 2000，总线驱动程序必须调用**PoStartNextPowerIrp**一次为每个[ **IRP\_MN\_查询\_电源** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)或[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)驱动程序收到的请求。

总线驱动程序始终调用该例程中其*DispatchPower*例程中，调用之前[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)例程。

 

 




