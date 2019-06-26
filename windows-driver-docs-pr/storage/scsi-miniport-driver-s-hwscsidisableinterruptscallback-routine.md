---
title: SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程
description: SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程
ms.assetid: d6c668cc-cb8d-42f4-a6e0-74bbd8b1b27a
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiDisableInterruptsCallback
- HwScsiDisableInterruptsCallback
- 中断 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c1c13987a6f392e94bc0ea22ec212ef4289a05e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384324"
---
# <a name="scsi-miniport-drivers-hwscsidisableinterruptscallback-routine"></a>SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程


## <span id="ddk_scsi_miniport_drivers_hwscsidisableinterruptscallback_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDISABLEINTERRUPTSCALLBACK_ROUTINE_KG"></span>


[ **HwScsiDisableInterruptsCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557288(v=vs.85))例程应执行以下操作：

-   重新启用来自 HBA 的中断

-   返回控件

请注意，此例程必须尽可能避免在计算机中使用其他设备的 I/O 操作快地执行。 因此， *HwScsiDisableInterruptsCallback*必须执行不是重新启用 HBA 上的中断，会将控件返回之前没有更多。

 

 




