---
title: SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程
description: SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiDisableInterruptsCallback
- HwScsiDisableInterruptsCallback
- 中断 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 503448343bc0c4dbe1e38a94ac210b4d35bd5a75
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821827"
---
# <a name="scsi-miniport-drivers-hwscsidisableinterruptscallback-routine"></a>SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程


## <span id="ddk_scsi_miniport_drivers_hwscsidisableinterruptscallback_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDISABLEINTERRUPTSCALLBACK_ROUTINE_KG"></span>


[**HwScsiDisableInterruptsCallback**](/previous-versions/windows/hardware/drivers/ff557288(v=vs.85))例程应执行以下操作：

-   从 HBA 重新启用中断

-   返回控件

请注意，此例程必须尽快执行，以避免对计算机中的其他设备使用 i/o 操作。 因此， *HwScsiDisableInterruptsCallback* 在返回 control 之前，必须在 HBA 上执行的操作不能超过重新启用中断。

 

