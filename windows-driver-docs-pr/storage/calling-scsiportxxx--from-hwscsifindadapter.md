---
title: 从 HwScsiFindAdapter 调用 ScsiPortXxx
description: 从 HwScsiFindAdapter 调用 ScsiPortXxx
ms.assetid: 17cfca31-ff93-4882-872c-ab8af6cdc3cf
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储，HwScsiFindAdapter
- 调用 ScsiPortXxx 例程 WDK 存储
- ScsiPortXxx 调用
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: a4ea7f92531de8c4d70206164641cf8a9d107752
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252445"
---
# <a name="calling-scsiportxxx-from-hwscsifindadapter"></a>从 HwScsiFindAdapter 调用 ScsiPortXxx

某些**ScsiPort**_Xxx_例程只能通过微型端口驱动程序的*HwScsiFindAdapter* *例程调用，* 具体如下所示：

- [**ScsiPortValidateRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportvalidaterange)验证是否尚未在注册表中通过另一台设备的驱动程序来声明微型端口驱动程序提供的总线相关访问范围。

- [**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)用于将 HBA 的（总线相关） "物理" 地址范围映射到系统分配的逻辑地址范围，驱动程序可通过调用**ScsiPortRead**_Xxx_和**ScsiPortWrite**_Xxx_例程，其中包含映射的逻辑范围地址。

- 如果*HwScsiFindAdapter*在给定 i/o 总线上找不到可支持的 HBA （如端口 @ NO__T-3CONFIGURATION @ NO__T-4INFORMATION **SystemIoBusNumber**值所示），则[**ScsiPortFreeDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportfreedevicebase)释放此类映射范围。

- [**ScsiPortGetUncachedExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetuncachedextension)分配系统和总线主机 HBA 之间共享的 DMA 缓冲区。

除了这四个例程以外，还有一个例程只能从微型端口驱动程序的*HwScsiFindAdapter*例程调用，*或*在控件类型为**ScsiSetRunningConfig**时从*HwScsiAdapterControl*调用：

- [**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata)获取特定于 BUS_DATA_TYPE 的配置信息，例如，总线相关设备内存（访问）范围、中断矢量或 IRQL 以及 DMA 通道或端口。

有关这些**ScsiPort**_Xxx_例程的详细信息，请参阅[SCSI 端口驱动程序支持例程](scsi-port-driver-support-routines.md)。
