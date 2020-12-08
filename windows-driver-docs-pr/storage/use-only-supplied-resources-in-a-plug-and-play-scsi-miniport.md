---
title: 在即插即用 SCSI 微型端口中只使用供应的资源
description: 在即插即用 SCSI 微型端口中只使用供应的资源
keywords:
- SCSI 微型端口驱动程序 WDK 存储，PnP
- PnP WDK SCSI
- 即插即用 WDK SCSI
- 转换 SCSI 微型端口驱动程序
- 资源限制 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abd4f05ebde22b8e7a462cb4bb5be54f1f258d23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790343"
---
# <a name="use-only-supplied-resources-in-a-plug-and-play-scsi-miniport"></a>在即插即用 SCSI 微型端口中只使用供应的资源


## <span id="ddk_use_only_supplied_resources_in_a_plug_and_play_scsi_miniport_kg"></span><span id="DDK_USE_ONLY_SUPPLIED_RESOURCES_IN_A_PLUG_AND_PLAY_SCSI_MINIPORT_KG"></span>


即插即用系统的目标之一是通过访问已知的内存位置来减少或消除检测其设备的驱动程序的数量。 这包括通过读取 HBA 的配置空间来确定其资源的驱动程序。

在即插即用中，可枚举总线上的设备由总线的驱动程序检测。 这允许总线驱动程序处理任何资源冲突，为中断的总线和桥接部件提供特殊的修补程序。

因此，如果 Microsoft Windows 2000 和更高版本系统中有任何) ，则 SCSI 微型端口驱动程序必须仅使用端口驱动程序提供的资源 (。 仅当端口驱动程序传入零值访问范围时，才允许使用微型端口驱动程序扫描 HBA 的总线。 如果微型端口驱动程序尝试使用未分配给它的资源，则 [**ScsiPortGetDeviceBase**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase) 调用将失败。 对读取和写入未正确映射的设备寄存器或端口的调用也可能会失败。

 

