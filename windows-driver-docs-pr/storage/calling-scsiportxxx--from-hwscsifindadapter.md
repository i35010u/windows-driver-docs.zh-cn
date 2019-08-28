---
title: 从 HwScsiFindAdapter 调用 ScsiPortXxx
description: 从 HwScsiFindAdapter 调用 ScsiPortXxx
ms.assetid: 17cfca31-ff93-4882-872c-ab8af6cdc3cf
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储, HwScsiFindAdapter
- 调用 ScsiPortXxx 例程 WDK 存储
- ScsiPortXxx 调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 387e58d30a38d84473cf02e7ceaa01aef3a1143c
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063905"
---
# <a name="calling-scsiportxxx-from-hwscsifindadapter"></a>从 HwScsiFindAdapter 调用 ScsiPortXxx


## <span id="ddk_calling_scsiportxxx_from_hwscsifindadapter_kg"></span><span id="DDK_CALLING_SCSIPORTXXX_FROM_HWSCSIFINDADAPTER_KG"></span>


某些**ScsiPort**_Xxx_例程只能通过微型端口驱动程序的*HwScsiFindAdapter*例程调用, 具体如下所示:

-   [**ScsiPortValidateRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportvalidaterange)验证是否尚未在注册表中通过另一台设备的驱动程序来声明微型端口驱动程序提供的总线相关访问范围。

-   [**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)用于将 HBA 的 (总线相关) "物理" 地址范围映射到系统分配的逻辑地址范围, 驱动程序可通过调用**ScsiPortRead**_Xxx_和**ScsiPortWrite**_Xxx_例程, 其中包含映射的逻辑范围地址。

-   如果*HwScsiFindAdapter*在给定 i/o 总线上找不到可支持的 HBA, 则\_ [**ScsiPortFreeDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportfreedevicebase)发布此类映射范围, 如端口配置\_信息**SystemIoBusNumber**所示。负值.

-   [**ScsiPortGetUncachedExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetuncachedextension)分配系统和总线主机 HBA 之间共享的 DMA 缓冲区。

除了这四个例程, 还可以在控件类型为**ScsiSetRunningConfig**时, 仅可从微型端口驱动程序的*HwScsiFindAdapter*例程*或* *HwScsiAdapterControl*调用一个例程:

-   [**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata)获取特定于\_总线\_数据类型的配置信息, 例如, 总线相关设备内存 (访问) 范围、中断矢量或 IRQL 以及 DMA 通道或端口。

有关这些**ScsiPort**_Xxx_例程的详细信息, 请参阅[SCSI 端口库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

 

 




