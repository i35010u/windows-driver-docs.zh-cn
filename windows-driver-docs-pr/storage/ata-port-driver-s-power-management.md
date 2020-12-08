---
title: ATA 端口驱动程序的电源管理
description: ATA 端口驱动程序的电源管理
keywords:
- ATA 端口驱动程序 WDK，电源管理
- 电源管理 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc19c1c996222e9919fff120fd9a75c9e337889e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835363"
---
# <a name="ata-port-drivers-power-management"></a>ATA 端口驱动程序的电源管理


## <span id="ddk_ata_port_drivers_power_management_kg"></span><span id="DDK_ATA_PORT_DRIVERS_POWER_MANAGEMENT_KG"></span>


**注意** ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用 [storport 驱动](./storport-driver-overview.md) 程序和 [storport 微型端口](./storport-miniport-drivers.md) 驱动程序模型。


ATA 端口驱动程序使微型端口驱动程序可以更改单个 LUN 或单个通道上的电源状态。 若要更改 LUN 的电源状态，ATA 端口驱动程序会将函数值为 IRB 的 IRB 发送 \_ \_ \_ 到设备驱动程序。 IRB 的 **PowerChange** 成员指示当前和目标电源状态。 若要更改整个通道的电源状态，端口驱动程序将调用 [**IdeHwControl**](/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_control) 微型端口驱动程序例程。

微型端口驱动程序可以通过调用 [**AtaPortRequestPowerStateChange**](/windows-hardware/drivers/ddi/irb/nf-irb-ataportrequestpowerstatechange)开始电源状态转换。 小型端口驱动程序可以在此之后（例如，在 IDE 设备的热插拔）之后调用此例程。

强烈建议不要通过微型端口驱动程序执行空闲检测。

