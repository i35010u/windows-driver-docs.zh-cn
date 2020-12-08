---
title: SCSI 微型端口驱动程序的 HwScsiInitialize 例程
description: SCSI 微型端口驱动程序的 HwScsiInitialize 例程
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiInitialize
- HwScsiInitialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee4668fecde4eee34a307bdedcd063aaa443a2db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828411"
---
# <a name="scsi-miniport-drivers-hwscsiinitialize-routine"></a>SCSI 微型端口驱动程序的 HwScsiInitialize 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiinitialize_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIINITIALIZE_ROUTINE_KG"></span>


对于微型端口驱动程序找到的每个受支持的 HBA，会调用其 [*HwScsiInitialize*](/previous-versions/windows/hardware/drivers/ff557302(v=vs.85)) 例程来设置 HBA 的寄存器和初始状态（如果有）。

如果 *HwScsiInitialize* 例程在 HBA 上启用中断，则将调用微型端口驱动程序的 [**HwScsiInterrupt**](/previous-versions/windows/hardware/drivers/ff557312(v=vs.85)) 例程来处理设备在初始化期间生成的任何中断。

如果初始化 HBA 导致总线重置， *HwScsiInitialize* 例程必须调用具有 *NotificationType* 值 **ResetDetected** 的 [**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 。

 

