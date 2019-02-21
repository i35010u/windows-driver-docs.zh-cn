---
title: SCSI 微型端口驱动程序的 HwScsiInitialize 例程
description: SCSI 微型端口驱动程序的 HwScsiInitialize 例程
ms.assetid: 2a776c0a-1bac-4f8c-beab-fd53300f68c8
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiInitialize
- HwScsiInitialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb53bff091d90541f1c67f5b13f51b900920f476
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524253"
---
# <a name="scsi-miniport-drivers-hwscsiinitialize-routine"></a>SCSI 微型端口驱动程序的 HwScsiInitialize 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiinitialize_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIINITIALIZE_ROUTINE_KG"></span>


对于每种支持 HBA 发现的微型端口驱动程序，其[ *HwScsiInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff557302)例程调用以设置 HBA 的寄存器和初始状态，如果有的话。

如果*HwScsiInitialize*例程启用 HBA 上，微型端口驱动程序的中断[ **HwScsiInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff557312)例程将调用以处理任何中断的设备在初始化期间生成。

如果初始化 HBA 导致总线重置*HwScsiInitialize*例程必须调用[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)与*NotificationType*值**ResetDetected**。

 

 




