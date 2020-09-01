---
title: 在检测期间验证 HwScsiFindAdapter 中的资源范围
description: 在检测期间验证 HwScsiFindAdapter 中的资源范围
ms.assetid: 2909aac2-714e-4353-8006-06cf68e4dfc8
keywords:
- SCSI 微型端口驱动程序 WDK 存储，PnP
- PnP WDK SCSI
- 即插即用 WDK SCSI
- 转换 SCSI 微型端口驱动程序
- 资源范围 WDK SCSI
- HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a9dd79e1dd33ae76da7c0ef62bd358afac12a8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191629"
---
# <a name="verify-resource-ranges-in-hwscsifindadapter-during-detection"></a>在检测期间验证 HwScsiFindAdapter 中的资源范围


## <span id="ddk_verify_resource_ranges_in_hwscsifindadapter_during_detection_kg"></span><span id="DDK_VERIFY_RESOURCE_RANGES_IN_HWSCSIFINDADAPTER_DURING_DETECTION_KG"></span>


尽管在即插即用中通常不需要检测设备，但是端口驱动程序可能会调用即插即用微型端口驱动程序的 [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 例程来检测 nonenumerable 总线上的设备。 尽管此操作与 Microsoft Windows NT 4.0 中的检测类似，但微型端口驱动程序必须注意不要对可能由另一设备使用的范围进行操作。

在调用[**ScsiPortGetDeviceBase**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase)之前，微型端口驱动程序应调用[**ScsiPortValidateRange**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportvalidaterange) ，以确保微型端口驱动程序提供的范围可以安全使用。 微型端口驱动程序必须准备好 **ScsiPortGetDeviceBase** ，并返回 **NULL** 指针。 微型端口驱动程序还应避免从地址零开始映射内存，这使得无法在某些系统上检测 **ScsiPortGetDeviceBase** 的失败。

 

