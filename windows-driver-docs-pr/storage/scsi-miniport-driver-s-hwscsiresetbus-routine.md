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
ms.openlocfilehash: 27df15eaa9e0614174581c6f1415989241686a57
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187795"
---
# <a name="scsi-miniport-drivers-hwscsiresetbus-routine"></a>SCSI 微型端口驱动程序的 HwScsiResetBus 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiresetbus_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIRESETBUS_ROUTINE_KG"></span>


每个微型端口驱动程序都必须有一个 [*HwScsiResetBus*](/previous-versions/windows/hardware/drivers/ff557318(v=vs.85)) 例程，该例程通过指向用于 HBA 状态的微型端口驱动程序的设备扩展的指针和要重置的总线的 **PathId** 进行调用。 如果尝试的总线重置操作失败或超时，微型端口驱动程序应调用 [**ScsiPortLogError**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportlogerror) ，然后对 HBA 进行重置。

总线重置操作可能要求微型端口驱动程序清除它在设备扩展中维护的状态和/或总线上设备的逻辑单元扩展。 *HwScsiResetBus*必须通过以下方式完成任何未完成的请求：使用**SrbStatus**值 SRB 状态总线重置调用[**ScsiPortCompleteRequest**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportcompleterequest) ， \_ \_ 或通过 \_ 此状态值为单独 SRBs、 [**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)调用。

完成总线重置请求和任何未完成的请求后，微型端口驱动程序必须调用 **ScsiPortNotification** () 如果尚未通过 * NotificationType ***NextRequest**，则为; 如果 HBA 支持标记队列或每个逻辑单元多个请求，则为 **NextLuRequest** 。

请注意，特定于操作系统的端口驱动程序会代表微型端口驱动程序管理 SCSI 总线重置延迟。

 

