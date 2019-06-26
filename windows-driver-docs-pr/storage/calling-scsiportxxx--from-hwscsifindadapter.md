---
title: 从 HwScsiFindAdapter 调用 ScsiPortXxx
description: 从 HwScsiFindAdapter 调用 ScsiPortXxx
ms.assetid: 17cfca31-ff93-4882-872c-ab8af6cdc3cf
keywords:
- HwScsiFindAdapter
- SCSI 微型端口驱动程序 WDK 存储 HwScsiFindAdapter
- 调用 ScsiPortXxx 例程 WDK 存储
- ScsiPortXxx 调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33db0ecffeea18322961635cf2362d380fa32965
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368353"
---
# <a name="calling-scsiportxxx-from-hwscsifindadapter"></a>从 HwScsiFindAdapter 调用 ScsiPortXxx


## <span id="ddk_calling_scsiportxxx_from_hwscsifindadapter_kg"></span><span id="DDK_CALLING_SCSIPORTXXX_FROM_HWSCSIFINDADAPTER_KG"></span>


某些 **ScsiPort * * * Xxx*可以调用例程*仅*微型端口驱动程序从*HwScsiFindAdapter* routine(s)，具体而言，以下：

-   [**ScsiPortValidateRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportvalidaterange)若要验证的微型端口驱动程序提供，总线相对访问范围不已声明在注册表中的另一个其设备驱动程序。

-   [**ScsiPortGetDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)要映射的 （总线相对）"物理"地址范围的驱动程序可用于通过调用 HBA 与通信在系统分配的逻辑地址范围的 HBA **ScsiPortRead * * * Xxx*和 **ScsiPortWrite * * * Xxx*例程与映射的逻辑范围地址。

-   [**ScsiPortFreeDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportfreedevicebase)释放此类映射的范围，如果*HwScsiFindAdapter*找不到它可以支持在给定 I/O 总线的 HBA 端口所示\_配置\_信息**SystemIoBusNumber**值。

-   [**ScsiPortGetUncachedExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetuncachedextension)来分配系统和总线 master HBA 之间共享 DMA 缓冲区。

除了这些四种例程，还有一个仅可从微型端口驱动程序的调用的例程*HwScsiFindAdapter*例程*或*从*HwScsiAdapterControl*当控件类型是**ScsiSetRunningConfig**:

-   [**ScsiPortGetBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata)若要获取总线\_数据\_特定于类型的配置信息，例如总线相对设备内存 （访问） 范围、 中断矢量或 irql，因此和 DMA 通道或端口。

有关这些详细信息 **ScsiPort * * * Xxx*例程，请参阅[SCSI 端口库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

 

 




