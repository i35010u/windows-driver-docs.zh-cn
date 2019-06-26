---
title: Unload 例程的功能
description: Unload 例程的功能
ms.assetid: a36b4687-df1d-498f-b9f3-d13ae2a9a3cd
keywords:
- 卸载例程 WDK 内核，功能
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fcaa08f6446af35f7ce40b1b70f900c2c94265a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382932"
---
# <a name="unload-routine-functionality"></a>Unload 例程的功能





驱动程序的职责[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程依赖于该驱动程序是否支持即插即用。

就像[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程的即插即用驱动程序通常简单，因此是其*卸载*例程，如中所述[即插即用驱动程序的卸载例程](pnp-driver-s-unload-routine.md).

非 PnP 驱动程序的*Unload*例程必须释放设备对象并释放驱动程序分配资源。 简单地说，它必须撤消执行其对应的工作**DriverEntry**并[*重新初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)中初始化该驱动程序、 其设备和其资源的例程。 请参阅[非 PnP 驱动程序的卸载例程](non-pnp-driver-s-unload-routine.md)有关详细信息。

 

 




