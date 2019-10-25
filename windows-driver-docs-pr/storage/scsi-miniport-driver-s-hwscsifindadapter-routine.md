---
title: SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程
description: SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程
ms.assetid: c89ad751-ff29-4aa7-b907-cb490d060906
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ca3badd855d43ebf226442fcb8d892a6066cce8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842670"
---
# <a name="scsi-miniport-drivers-hwscsifindadapter-routine"></a>SCSI 微型端口驱动程序的 HwScsiFindAdapter 例程


## <span id="ddk_scsi_miniport_drivers_hwscsifindadapter_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIFINDADAPTER_ROUTINE_KG"></span>


操作系统特定的端口驱动程序在配置信息缓冲区中尽可能多地填入[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)，因为它可以从微型端口驱动程序的[**硬件\_初始化\_数据（SCSI）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)规范和系统中的其他源，然后再调用给定*HwScsiFindAdapter*例程，并使用指向配置信息缓冲区的指针。

通常情况下， *HwScsiFindAdapter*例程负责使用提供的配置信息和/或调用 **ScsiPort * * * Xxx*来收集足够的配置信息，以确定它是否支持 i/o 上的 HBA端口\_配置中的**SystemIoBusNumber**标识的总线\_端口驱动程序提供的信息。 如果是这样，则*HwScsiFindAdapter*负责在端口\_配置\_信息中为所支持的 HBA 填写任何剩余的配置信息，以便通过驱动程序确定了该 HBA 的状态，并在它返回 control 之前，将*该参数设置为适当的值*。

有关详细信息，请参阅[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)和[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 。

 

 




