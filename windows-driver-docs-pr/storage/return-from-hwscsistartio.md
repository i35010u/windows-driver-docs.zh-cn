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
ms.openlocfilehash: a3178ad26c7ccac2e0ee808f1a1d898d58ca92f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842688"
---
# <a name="return-from-hwscsistartio"></a>从 HwScsiStartIo 返回


## <span id="ddk_return_from_hwscsistartio_kg"></span><span id="DDK_RETURN_FROM_HWSCSISTARTIO_KG"></span>


每个[**HwScsiStartIo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))例程必须返回**TRUE**，指示已处理输入请求。

如果*HwScsiStartIo*例程在调用时无法执行请求的操作，则*HwScsiStartIo*应执行以下操作：

1.  将输入 SRB 的**SrbStatus**设置为 SRB\_状态\_"忙碌"。

2.  将[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)与*NotificationType * * * RequestComplete** 和输入 SRB 一起调用。

3.  如果驱动程序可以接受与刚完成的 SRB 中的目标逻辑单元不同的目标逻辑单元的请求，请使用*NotificationType * * * NextRequest** 调用**ScsiPortNotification** 。

4.  返回**TRUE**。

端口驱动程序将重新提交**SrbStatus**值为 SRB\_状态的任何请求，然后再重新提交微型端口驱动程序的*HWSCSISTARTIO*例程\_繁忙状态。

最终，每个微型端口驱动程序必须为每个 SRB 输入对其*HwScsiStartIo*例程调用两次**ScsiPortNotification** ：第一次是完成请求（*NotificationType ***RequestComplete**），并将为，则在下一个 SRB （* NotificationType ***NextRequest**或**NextLuRequest**）中再次调用 HwScsiStartIo 例程。

小型端口驱动程序的*HwScsiStartIo*例程，该例程通过使用*NotificationType * * * RequestTimerCall** 和指向其*HwScsiTimer*例程的指针轮询调用**ScsiPortNotification**来专门管理其 HBA。 有关*HwScsiTimer*例程的详细信息，请参阅[SCSI 微型端口驱动程序的 HwScsiTimer 例程](scsi-miniport-driver-s-hwscsitimer-routine.md)。

 

 




