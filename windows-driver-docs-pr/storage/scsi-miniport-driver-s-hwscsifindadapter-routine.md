---
title: SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程
description: SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程
ms.assetid: c89ad751-ff29-4aa7-b907-cb490d060906
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储 HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe8a1217bab4dfc0eb5362a974b3d7272bdc0e1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385226"
---
# <a name="scsi-miniport-drivers-hwscsifindadapter-routine"></a>SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程


## <span id="ddk_scsi_miniport_drivers_hwscsifindadapter_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIFINDADAPTER_ROUTINE_KG"></span>


特定于操作系统的端口驱动程序会填写尽可能[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)作为它的配置信息缓冲区中可以从微型端口驱动程序[ **HW\_初始化\_数据 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)规范，然后才能调用系统中的其他源给定*HwScsiFindAdapter*例程替换指向配置信息缓冲区的指针。

一般情况下， *HwScsiFindAdapter*例程负责使用提供的配置信息和/或调用 **ScsiPort * * * Xxx*收集到足够的配置信息确定是否它由标识在 I/O 总线上支持 HBA **SystemIoBusNumber**在端口\_配置\_提供端口驱动程序的信息。 如果是这样， *HwScsiFindAdapter*负责在受支持的 HBA 端口中的任何其余配置信息填写\_配置\_的设置微型端口驱动程序的信息使用驱动程序确定状态的 HBA，以及设置的设备扩展*Again*为适当的值之前会将控件返回的参数。

请参阅[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)并[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))有关详细信息。

 

 




