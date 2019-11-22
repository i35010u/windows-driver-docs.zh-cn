---
title: SCSI 微型端口驱动程序的 HwScsiResetBus 例程
description: SCSI 微型端口驱动程序的 HwScsiResetBus 例程
ms.assetid: ca4ab3e6-e23c-443a-bcf6-6fd516569999
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiResetBus
- HwScsiResetBus
- 总线重置操作 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96e53ffddf35142195f6ec74f62608e7190420d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842665"
---
# <a name="scsi-miniport-drivers-hwscsiresetbus-routine"></a>SCSI 微型端口驱动程序的 HwScsiResetBus 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiresetbus_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIRESETBUS_ROUTINE_KG"></span>


每个微型端口驱动程序都必须有一个[*HwScsiResetBus*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))例程，该例程通过指向用于 HBA 状态的微型端口驱动程序的设备扩展的指针和要重置的总线的**PathId**进行调用。 如果尝试的总线重置操作失败或超时，微型端口驱动程序应调用[**ScsiPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportlogerror) ，然后对 HBA 进行重置。

总线重置操作可能要求微型端口驱动程序清除它在设备扩展中维护的状态和/或总线上设备的逻辑单元扩展。 *HwScsiResetBus*必须通过以下方式完成所有未完成的请求：使用**SrbStatus**值 SRB\_状态\_总线\_RESET，或使用此状态值为单独的 SRBs、 [**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)调用[**ScsiPortCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportcompleterequest) 。

完成总线重置请求和任何未完成的请求后，微型端口驱动程序必须通过 * NotificationType ***NextRequest**（如果尚未执行此操作）调用**ScsiPortNotification** （如果尚未执行此操作） **，如果 HBA**支持标记队列或每个逻辑单元的多个请求。

请注意，特定于操作系统的端口驱动程序会代表微型端口驱动程序管理 SCSI 总线重置延迟。

 

 




