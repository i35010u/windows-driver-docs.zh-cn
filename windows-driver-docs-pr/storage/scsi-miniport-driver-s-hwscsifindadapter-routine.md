---
title: SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程
description: SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程
ms.assetid: c89ad751-ff29-4aa7-b907-cb490d060906
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储 HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3dea9567022abb481e6dbcacc6b9774ce24e469
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519033"
---
# <a name="scsi-miniport-drivers-hwscsifindadapter-routine"></a>SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程


## <span id="ddk_scsi_miniport_drivers_hwscsifindadapter_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIFINDADAPTER_ROUTINE_KG"></span>


特定于操作系统的端口驱动程序会填写尽可能[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563900)作为它的配置信息缓冲区中可以从微型端口驱动程序[ **HW\_初始化\_数据 (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff557456)规范，然后才能调用系统中的其他源给定*HwScsiFindAdapter*例程替换指向配置信息缓冲区的指针。

一般情况下， *HwScsiFindAdapter*例程负责使用提供的配置信息和/或调用 **ScsiPort * * * Xxx*收集到足够的配置信息确定是否它由标识在 I/O 总线上支持 HBA **SystemIoBusNumber**在端口\_配置\_提供端口驱动程序的信息。 如果是这样， *HwScsiFindAdapter*负责在受支持的 HBA 端口中的任何其余配置信息填写\_配置\_的设置微型端口驱动程序的信息使用驱动程序确定状态的 HBA，以及设置的设备扩展*Again*为适当的值之前会将控件返回的参数。

请参阅[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563900)并[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)有关详细信息。

 

 




