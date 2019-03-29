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
ms.openlocfilehash: 8f3251caebd4ac64a2cec2c3daa4e877bbc3ee6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568757"
---
# <a name="calling-scsiportxxx-from-hwscsifindadapter"></a>从 HwScsiFindAdapter 调用 ScsiPortXxx


## <span id="ddk_calling_scsiportxxx_from_hwscsifindadapter_kg"></span><span id="DDK_CALLING_SCSIPORTXXX_FROM_HWSCSIFINDADAPTER_KG"></span>


某些 **ScsiPort * * * Xxx*可以调用例程*仅*微型端口驱动程序从*HwScsiFindAdapter* routine(s)，具体而言，以下：

-   [**ScsiPortValidateRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564761)若要验证的微型端口驱动程序提供，总线相对访问范围不已声明在注册表中的另一个其设备驱动程序。

-   [**ScsiPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564629)要映射的 （总线相对）"物理"地址范围的驱动程序可用于通过调用 HBA 与通信在系统分配的逻辑地址范围的 HBA **ScsiPortRead * * * Xxx*和 **ScsiPortWrite * * * Xxx*例程与映射的逻辑范围地址。

-   [**ScsiPortFreeDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564623)释放此类映射的范围，如果*HwScsiFindAdapter*找不到它可以支持在给定 I/O 总线的 HBA 端口所示\_配置\_信息**SystemIoBusNumber**值。

-   [**ScsiPortGetUncachedExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff564639)来分配系统和总线 master HBA 之间共享 DMA 缓冲区。

除了这些四种例程，还有一个仅可从微型端口驱动程序的调用的例程*HwScsiFindAdapter*例程*或*从*HwScsiAdapterControl*当控件类型是**ScsiSetRunningConfig**:

-   [**ScsiPortGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff564624)若要获取总线\_数据\_特定于类型的配置信息，例如总线相对设备内存 （访问） 范围、 中断矢量或 irql，因此和 DMA 通道或端口。

有关这些详细信息 **ScsiPort * * * Xxx*例程，请参阅[SCSI 端口库例程](https://msdn.microsoft.com/library/windows/hardware/ff565375)。

 

 




