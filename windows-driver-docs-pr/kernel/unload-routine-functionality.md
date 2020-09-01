---
title: Unload 例程的功能
description: Unload 例程的功能
ms.assetid: a36b4687-df1d-498f-b9f3-d13ae2a9a3cd
keywords:
- 卸载例程，WDK 内核，功能
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7d46760cf0c6e7055cb521dee49eda041c1453f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185781"
---
# <a name="unload-routine-functionality"></a>Unload 例程的功能





驱动程序的 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程的责任取决于驱动程序是否支持 PnP。

正如 PnP 驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程通常是简单的一样，它是其 *卸载* 例程，如 [Pnp 驱动程序的卸载例程](pnp-driver-s-unload-routine.md)中所述。

非 PnP 驱动程序的 *卸载* 例程必须释放设备对象和释放驱动程序分配的资源。 简而言之，它必须撤消其相应 **DriverEntry** 执行的工作，并在初始化驱动程序、其设备和资源时重新 [*初始化*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize) 例程。 有关详细信息，请参阅 [非 PnP 驱动程序的卸载例程](non-pnp-driver-s-unload-routine.md) 。

 

