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
ms.openlocfilehash: 3e589f8b1b3cc51f60c515f3e612192797575fbe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368398"
---
# <a name="ata-port-drivers-reset-mechanism"></a>ATA 端口驱动程序的重置机制


## <span id="ddk_ata_port_drivers_reset_mechanism_kg"></span><span id="DDK_ATA_PORT_DRIVERS_RESET_MECHANISM_KG"></span>

**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。



ATA 端口驱动程序支持类似于在某些方面，Storport 驱动程序的重置机制的两层重置机制。 重置机制 Storport 有关的详细信息，请参阅[多层重置在 Storport](multi-tier-reset-in-storport.md)。

如 Storport 驱动程序，并与 SCSI 端口驱动程序不同，避免了 ATA 端口驱动程序，只要有可能重置整个总线。 ATA 端口驱动程序首先尝试使用 IRB IRB 函数值重置单个 LUN\_函数\_LUN\_重置。 如果重置失败，ATA 端口驱动程序会将整个总线重置。

例如，假设 ATA 端口驱动程序问题 IRB 重置 LUN 后一个 LUN 的未完成的请求超时。在响应此 LUN 重置，微型端口驱动程序执行设备重置操作时，如果硬件支持此功能，并完成包括重置 IRB LUN 上所有未完成的请求。 重置 IRB 不超时。 因此没有其他请求将颁发给该 LUN 如果微型端口驱动程序未完成重置 IRB。

重置 IRB 微型端口驱动程序时 (即完成 IRB 以外的任何状态重置 IRB\_状态\_成功)，ATA 端口驱动程序调用微型端口驱动程序[ **IdeHwReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_reset)例程，以重置整个通道。 然后，微型端口驱动程序必须完成该通道的所有未完成请求，并执行必要的操作来重置附加到该通道的设备在硬件上。

ATA 端口驱动程序不支持的设备有多个 Lun 的目标重置。

 

 


