---
title: SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程
description: SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程
ms.assetid: d6c668cc-cb8d-42f4-a6e0-74bbd8b1b27a
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiDisableInterruptsCallback
- HwScsiDisableInterruptsCallback
- 中断 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36234f3c97806ace7637e43f955bb988ac6c634
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183851"
---
# <a name="scsi-miniport-drivers-hwscsidisableinterruptscallback-routine"></a>SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程


## <span id="ddk_scsi_miniport_drivers_hwscsidisableinterruptscallback_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDISABLEINTERRUPTSCALLBACK_ROUTINE_KG"></span>


[**HwScsiDisableInterruptsCallback**](/previous-versions/windows/hardware/drivers/ff557288(v=vs.85))例程应执行以下操作：

-   从 HBA 重新启用中断

-   返回控件

请注意，此例程必须尽快执行，以避免对计算机中的其他设备使用 i/o 操作。 因此， *HwScsiDisableInterruptsCallback* 在返回 control 之前，必须在 HBA 上执行的操作不能超过重新启用中断。

 

