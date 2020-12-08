---
title: 从 HwScsiStartIo 返回
description: 从 HwScsiStartIo 返回
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- 返回值 WDK SCSI
- status 值 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a6ce7685e89bdffe5f6b0cbfd0e40254e8de326
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802205"
---
# <a name="return-from-hwscsistartio"></a>从 HwScsiStartIo 返回


## <span id="ddk_return_from_hwscsistartio_kg"></span><span id="DDK_RETURN_FROM_HWSCSISTARTIO_KG"></span>


每个 [**HwScsiStartIo**](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85)) 例程必须返回 **TRUE**，指示已处理输入请求。

如果 *HwScsiStartIo* 例程在调用时无法执行请求的操作，则 *HwScsiStartIo* 应执行以下操作：

1.  将输入 SRB 的 **SrbStatus** 设置为 SRB \_ 状态 " \_ 忙碌"。

2.  将 [**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 与 *NotificationType * * * RequestComplete** 和输入 SRB 一起调用。

3.  如果驱动程序可以接受与刚完成的 SRB 中的目标逻辑单元不同的目标逻辑单元的请求，请使用 *NotificationType * * * NextRequest** 调用 **ScsiPortNotification** 。

4.  返回 **TRUE**。

端口驱动程序稍后重新提交 **SrbStatus** 值 SRB \_ 状态 \_ 为 "忙碌" *的任何* 请求。

最终，每个微型端口驱动程序必须为每个 SRB 输入对其 *HwScsiStartIo* 例程调用两次 **ScsiPortNotification** ：第一次是 (*NotificationType ***RequestComplete**) 第二次调用，然后告诉端口驱动程序再次调用 *HwScsiStartIo* 例程， (* NotificationType ***SRB** 或 **NextRequest**) 。

小型端口驱动程序的 *HwScsiStartIo* 例程，该例程通过使用 *NotificationType * * * RequestTimerCall** 和指向其 *HwScsiTimer* 例程的指针轮询调用 **ScsiPortNotification** 来专门管理其 HBA。 有关 *HwScsiTimer* 例程的详细信息，请参阅 [SCSI 微型端口驱动程序的 HwScsiTimer 例程](scsi-miniport-driver-s-hwscsitimer-routine.md)。

 

