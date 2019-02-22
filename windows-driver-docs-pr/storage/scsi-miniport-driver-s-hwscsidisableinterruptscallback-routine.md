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
ms.openlocfilehash: 6713a8cf8932467aec5c612c9f6b826a9520fb0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534843"
---
# <a name="scsi-miniport-drivers-hwscsidisableinterruptscallback-routine"></a>SCSI 微型端口驱动程序的 HwScsiDisableInterruptsCallback 例程


## <span id="ddk_scsi_miniport_drivers_hwscsidisableinterruptscallback_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIDISABLEINTERRUPTSCALLBACK_ROUTINE_KG"></span>


[ **HwScsiDisableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557288)例程应执行以下操作：

-   重新启用来自 HBA 的中断

-   返回控件

请注意，此例程必须尽可能避免在计算机中使用其他设备的 I/O 操作快地执行。 因此， *HwScsiDisableInterruptsCallback*必须执行不是重新启用 HBA 上的中断，会将控件返回之前没有更多。

 

 




