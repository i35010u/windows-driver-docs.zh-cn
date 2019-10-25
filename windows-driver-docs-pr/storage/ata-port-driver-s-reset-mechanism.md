---
title: ATA 端口驱动程序的重置机制
description: ATA 端口驱动程序的重置机制
ms.assetid: adc27819-d1ae-4b97-8109-5d742c0595d3
keywords:
- ATA 端口驱动程序 WDK，重置机制
- 重置机制 WDK ATA 端口驱动程序
- LUN 重置 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37df2d3374bb4600a8504427c0bcb3ed14ec2c28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845097"
---
# <a name="ata-port-drivers-reset-mechanism"></a>ATA 端口驱动程序的重置机制


## <span id="ddk_ata_port_drivers_reset_mechanism_kg"></span><span id="DDK_ATA_PORT_DRIVERS_RESET_MECHANISM_KG"></span>

**注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用[storport 驱动](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)程序和[storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。



ATA 端口驱动程序支持两层重置机制，这种机制在某些方面与 Storport 驱动程序的重置机制类似。 有关 Storport 重置机制的详细信息，请参阅[Storport 中的多层重置](multi-tier-reset-in-storport.md)。

与 Storport 驱动程序和 SCSI 端口驱动程序不同，ATA 端口驱动程序可避免在任何可能的情况下重置整个总线。 ATA 端口驱动程序首先尝试使用函数值为 IRB\_\_函数的 IRB 重置单个 LUN\_重置。 如果重置失败，ATA 端口驱动程序将重置整个总线。

例如，假设 ATA 端口驱动程序在某个 LUN 的未完成请求超时后发出 IRB 来重置 LUN。为响应此 LUN 重置，微型端口驱动程序将执行设备重置操作（如果硬件支持），并在 LUN 上完成所有未完成的请求，包括重置 IRB。 Reset IRB 未计时。 因此，如果微型端口驱动程序未完成 reset IRB，则不会向 LUN 发出额外的请求。

如果微型端口驱动程序失败，则重置 IRB （即，在 IRB\_状态之外的任何状态中完成 reset IRB\_SUCCESS），ATA 端口驱动程序将调用微型端口驱动程序的[**IdeHwReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_reset)例程来重置整个通道。 然后，微型端口驱动程序必须完成该通道的所有未完成的请求，并在硬件上执行必要的操作以重置连接到该通道的设备。

ATA 端口驱动程序不支持具有多个 Lun 的设备的目标重置。

 

 


