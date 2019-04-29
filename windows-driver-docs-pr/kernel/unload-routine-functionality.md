---
title: Unload 例程的功能
description: Unload 例程的功能
ms.assetid: a36b4687-df1d-498f-b9f3-d13ae2a9a3cd
keywords:
- 卸载例程 WDK 内核，功能
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f67e9d6499af2cd412fdf69508b7ce5613267d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355284"
---
# <a name="unload-routine-functionality"></a>Unload 例程的功能





驱动程序的职责[ *Unload* ](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程依赖于该驱动程序是否支持即插即用。

就像[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程的即插即用驱动程序通常简单，因此是其*卸载*例程，如中所述[即插即用驱动程序的卸载例程](pnp-driver-s-unload-routine.md).

非 PnP 驱动程序的*Unload*例程必须释放设备对象并释放驱动程序分配资源。 简单地说，它必须撤消执行其对应的工作**DriverEntry**并[*重新初始化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)中初始化该驱动程序、 其设备和其资源的例程。 请参阅[非 PnP 驱动程序的卸载例程](non-pnp-driver-s-unload-routine.md)有关详细信息。

 

 




