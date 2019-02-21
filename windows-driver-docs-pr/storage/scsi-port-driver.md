---
title: SCSI 端口驱动程序
description: SCSI 端口驱动程序
ms.assetid: e97ea5f2-7f20-4d3d-82a2-7d83e1eba30e
keywords:
- 存储端口驱动程序 WDK，SCSI 端口驱动程序
- SCSI 端口驱动程序 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143c54eb27bfb203d03cc951499d1de284ca57f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546883"
---
# <a name="scsi-port-driver"></a>SCSI 端口驱动程序


## <span id="ddk_scsi_port_driver_kg"></span><span id="DDK_SCSI_PORT_DRIVER_KG"></span>


Microsoft 提供的 Microsoft Windows 存储体系结构的标准功能的 SCSI 端口驱动程序。 SCSI 端口驱动程序模拟一个简化的 SCSI 适配器来简化 Windows 存储子系统。 存储类驱动程序加载端口驱动程序之上。 这意味着，你可以使用每个 SCSI 适配器的唯一的硬件功能的最小问题，为 Windows 编写存储类驱动程序。

SCSI 端口驱动程序的模拟功能还允许你开发要简单得多的设计和代码比整体化端口驱动程序的微型驱动程序。 换而言之，使用 SCSI 端口驱动程序，可专注于开发处理您的适配器的特定功能的微型端口驱动程序。

若要使用 SCSI 端口支持例程，链接到一个 SCSI 端口支持库*scsiport.lib*或*scsiwmi.lib*。 这些 SCSI 端口库处理微型端口驱动程序和硬件抽象层 (HAL) 的操作系统之间的所有交互。 微型端口驱动程序必须未链接到 HAL 支持库中，直接*hal.lib*，也不应直接向链接*ntoskrnl.lib*或*libcntpr.lib*支持库。 执行此操作的 SCSI 微型端口驱动程序不适合 Windows 徽标。

以下各部分分别 SCSI 端口驱动程序的主要功能。

1.  [SCSI 端口提供的功能](capabilities-provided-by-scsi-port.md)

2.  [SCSI 端口的存储类驱动程序接口](scsi-port-s-interface-with-the-storage-class-driver.md)

3.  [SCSI 端口 SCSI 端口微型端口驱动程序接口](scsi-port-s-interface-with-scsi-port-miniport-drivers.md)

4.  [SCSI 端口 I/O 模型](scsi-port-i-o-model.md)

中提供的 SCSI 端口微型端口驱动程序的一般讨论[SCSI 微型端口驱动程序](scsi-miniport-drivers.md)。

Windows 存储体系结构还提供了[Storport 驱动程序](storport-driver.md)，适用于高性能设备 SCSI 端口的替代方法。

 

 




