---
title: 在即插即用 SCSI 微型端口中只使用供应的资源
description: 在即插即用 SCSI 微型端口中只使用供应的资源
ms.assetid: 26c688dc-b6af-4a0c-8401-d53e653d90b3
keywords:
- SCSI 微型端口驱动程序 WDK 存储，即插即用
- 即插即用 WDK SCSI
- Plug and Play WDK SCSI
- 转换 SCSI 微型端口驱动程序
- 资源限制 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 870722da8a289979c9b6f42ce63c22b2a00a4ce5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386797"
---
# <a name="use-only-supplied-resources-in-a-plug-and-play-scsi-miniport"></a>在即插即用 SCSI 微型端口中只使用供应的资源


## <span id="ddk_use_only_supplied_resources_in_a_plug_and_play_scsi_miniport_kg"></span><span id="DDK_USE_ONLY_SUPPLIED_RESOURCES_IN_A_PLUG_AND_PLAY_SCSI_MINIPORT_KG"></span>


Plug and Play 系统的目标之一是减少或消除通过访问已知的内存位置检测到其设备的驱动程序的数量。 这包括通过读取其 HBA 配置空间来确定其资源的驱动程序。

在插，总线驱动程序检测到可枚举的总线上的设备。 这将允许总线驱动程序处理的任何资源冲突，中断的总线和桥部件等提供特殊处理的修补程序。

因此，SCSI 微型端口驱动程序必须使用在 Microsoft Windows 2000 和更高版本系统仅提供端口驱动程序 （如果有） 的资源。 微型端口驱动程序允许扫描在总线的 HBA，仅在端口驱动程序通过在零值的访问范围内。 如果尝试使用未分配给它，资源的微型端口驱动程序[ **ScsiPortGetDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)调用将失败。 调用以读取和写入设备注册或未映射正确的端口也可能会失败。

 

 




