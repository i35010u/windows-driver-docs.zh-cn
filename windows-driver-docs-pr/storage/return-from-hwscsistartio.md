---
title: 从 HwScsiStartIo 返回
description: 从 HwScsiStartIo 返回
ms.assetid: e3d5e21a-4dc2-41bf-97a2-9ac2aa5a1af2
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- 返回值 WDK SCSI
- 状态值 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8c57e337946cd1fd902b43fee19dfcb74266307
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325291"
---
# <a name="return-from-hwscsistartio"></a>从 HwScsiStartIo 返回


## <span id="ddk_return_from_hwscsistartio_kg"></span><span id="DDK_RETURN_FROM_HWSCSISTARTIO_KG"></span>


每个[ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)例程必须返回**TRUE**，，该值指示输入的请求已处理。

如果*HwScsiStartIo*例程不能执行请求的操作时调用它时， *HwScsiStartIo*应执行以下操作：

1.  设置输入 SRB 的**SrbStatus**到 SRB\_状态\_忙。

2.  调用[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)与*NotificationType * * * RequestComplete** 和 SRB 中的输入。

3.  调用**ScsiPortNotification**与*NotificationType * * * NextRequest** 如果该驱动程序可以接受的请求到不同目标逻辑单元中的一个比只是完成 SRB。

4.  返回 **，则返回 TRUE**。

端口驱动程序将重新提交任何请求返回与**SrbStatus**值 SRB\_状态\_微型端口驱动程序的繁忙*HwScsiStartIo*例程更高版本。

最终，每个微型端口驱动程序必须调用**ScsiPortNotification**两次对于每个 SRB 输入其*HwScsiStartIo*例程： 首先，需要完成的请求 (*NotificationType ***RequestComplete**) 和第二个，告知端口驱动程序来调用*HwScsiStartIo*再次与下一步 SRB 例程 (* NotificationType ***NextRequest**或**NextLuRequest**)。

*HwScsiStartIo*以独占方式通过轮询调用来管理其 HBA 的微型端口驱动程序的日常**ScsiPortNotification**与*NotificationType * * * RequestTimerCall** 和一个指向其*HwScsiTimer*例程。 有关详细信息*HwScsiTimer*例程，请参阅[SCSI 微型端口驱动程序 HwScsiTimer 例程](scsi-miniport-driver-s-hwscsitimer-routine.md)。

 

 




