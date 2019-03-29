---
title: ATA 端口驱动程序的电源管理
description: ATA 端口驱动程序的电源管理
ms.assetid: 01c37fed-3b5b-4dd9-bdbd-5c5499a2ddcf
keywords:
- ATA 端口驱动程序 WDK、 电源管理
- 电源管理 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41a4ad4b014f058c0e548d16bfcd2ea9b9e2e827
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563141"
---
# <a name="ata-port-drivers-power-management"></a>ATA 端口驱动程序的电源管理


## <span id="ddk_ata_port_drivers_power_management_kg"></span><span id="DDK_ATA_PORT_DRIVERS_POWER_MANAGEMENT_KG"></span>


**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。


ATA 端口驱动程序，若要更改在单独的 LUN 或单个通道上的电源状态的微型端口驱动程序。 若要更改的 LUN 电源状态，ATA 端口驱动程序，将发送函数值为 IRB IRB\_函数\_电源\_更改设备驱动程序。 **PowerChange** IRB 成员指示当前和目标的电源状态。 若要更改整个通道，端口驱动程序调用的电源状态[ **IdeHwControl** ](https://msdn.microsoft.com/library/windows/hardware/ff557465)微型端口驱动程序例程。

微型端口驱动程序可以通过调用开始电源状态转换[ **AtaPortRequestPowerStateChange**](https://msdn.microsoft.com/library/windows/hardware/ff550220)。 微型端口驱动程序之后，例如，热插拔 IDE 设备可能会调用此例程。

从微型端口驱动程序的空闲检测是强烈建议不要使用。

 

 


