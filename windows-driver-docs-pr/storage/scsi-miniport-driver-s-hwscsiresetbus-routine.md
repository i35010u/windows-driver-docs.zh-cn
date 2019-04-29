---
title: SCSI 微型端口驱动程序的 HwScsiResetBus 例程
description: SCSI 微型端口驱动程序的 HwScsiResetBus 例程
ms.assetid: ca4ab3e6-e23c-443a-bcf6-6fd516569999
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiResetBus
- HwScsiResetBus
- 总线重置期间 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9690e30a1a4169914e62fab843ca086add012fb3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378953"
---
# <a name="scsi-miniport-drivers-hwscsiresetbus-routine"></a>SCSI 微型端口驱动程序的 HwScsiResetBus 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiresetbus_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIRESETBUS_ROUTINE_KG"></span>


每个微型端口驱动程序必须具有[ *HwScsiResetBus* ](https://msdn.microsoft.com/library/windows/hardware/ff557318)例程，HBA 状态与指向微型端口驱动程序的设备扩展的调用并**PathId**的若要重置总线。 如果尝试的总线重置操作失败或超时，微型端口驱动程序应调用[ **ScsiPortLogError** ](https://msdn.microsoft.com/library/windows/hardware/ff564652) ，然后程序硬重置的 HBA。

总线重置操作可能需要微型端口驱动程序，以清理它保留在设备扩展和/或在总线上的设备的逻辑单元扩展的状态。 *HwScsiResetBus*必须完成所有未完成请求，通过调用[ **ScsiPortCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff564608)与**SrbStatus**值 SRB\_状态\_总线\_重置或为单个 Srb [ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)具有此状态的值。

完成后将总线重置请求和任何未完成的请求，微型端口驱动程序必须调用**ScsiPortNotification** （如果它具有这样做） 使用 * NotificationType ***NextRequest**，或**NextLuRequest**如果 HBA 支持有标记的队列或每个逻辑单元的多个请求。

请注意，在操作系统的特定端口驱动程序管理代表微型端口驱动程序的 SCSI 总线重置延迟。

 

 




