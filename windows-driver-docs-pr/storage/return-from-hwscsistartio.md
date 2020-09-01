---
title: 从 HwScsiStartIo 返回
description: 从 HwScsiStartIo 返回
ms.assetid: e3d5e21a-4dc2-41bf-97a2-9ac2aa5a1af2
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- 返回值 WDK SCSI
- status 值 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81e7d96887b97e8312dc13e28ddf5c6015c7516c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184179"
---
# <a name="return-from-hwscsistartio"></a>从 HwScsiStartIo 返回


## <span id="ddk_return_from_hwscsistartio_kg"></span><span id="DDK_RETURN_FROM_HWSCSISTARTIO_KG"></span>


每个 [**HwScsiStartIo**](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85)) 例程必须返回 **TRUE**，指示已处理输入请求。

如果 *HwScsiStartIo* 例程在调用时无法执行请求的操作，则 *HwScsiStartIo* 应执行以下操作：

1.  将输入 SRB 的 **SrbStatus** 设置为 SRB \_ 状态 " \_ 忙碌"。

2.  将 [**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 与 *NotificationType * * * RequestComplete** 和输入 SRB 一起调用。

3.  如果驱动程序可以接受与刚完成的 SRB 中的目标逻辑单元不同的目标逻辑单元的请求，请使用*NotificationType * * * NextRequest** 调用**ScsiPortNotification** 。

4.  返回 **TRUE**。

端口驱动程序稍后重新提交 **SrbStatus** 值 SRB \_ 状态 \_ 为 "忙碌" *的任何* 请求。

最终，每个微型端口驱动程序必须为每个 SRB 输入对其*HwScsiStartIo*例程调用两次**ScsiPortNotification** ：第一次是 (*NotificationType ***RequestComplete**) 第二次调用，然后告诉端口驱动程序再次调用*HwScsiStartIo*例程， (* NotificationType ***SRB**或**NextRequest**) 。

小型端口驱动程序的*HwScsiStartIo*例程，该例程通过使用*NotificationType * * * RequestTimerCall** 和指向其*HwScsiTimer*例程的指针轮询调用**ScsiPortNotification**来专门管理其 HBA。 有关 *HwScsiTimer* 例程的详细信息，请参阅 [SCSI 微型端口驱动程序的 HwScsiTimer 例程](scsi-miniport-driver-s-hwscsitimer-routine.md)。

 

