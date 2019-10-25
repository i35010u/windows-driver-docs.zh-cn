---
title: Unload 例程的功能
description: Unload 例程的功能
ms.assetid: a36b4687-df1d-498f-b9f3-d13ae2a9a3cd
keywords:
- 卸载例程，WDK 内核，功能
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6c136c052e47e516feaac2dfdb44c696fa6ab85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838376"
---
# <a name="unload-routine-functionality"></a>Unload 例程的功能





驱动程序的[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程的责任取决于驱动程序是否支持 PnP。

正如 PnP 驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程通常是简单的一样，它是其*卸载*例程，如[Pnp 驱动程序的卸载例程](pnp-driver-s-unload-routine.md)中所述。

非 PnP 驱动程序的*卸载*例程必须释放设备对象和释放驱动程序分配的资源。 简而言之，它必须撤消其相应**DriverEntry**执行的工作，并在初始化驱动程序、其设备和资源时重新[*初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)例程。 有关详细信息，请参阅[非 PnP 驱动程序的卸载例程](non-pnp-driver-s-unload-routine.md)。

 

 




