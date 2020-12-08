---
title: 支持 SCSI 微型端口驱动程序中的即插即用
description: 支持 SCSI 微型端口驱动程序中的即插即用
keywords:
- SCSI 微型端口驱动程序 WDK 存储，PnP
- PnP WDK SCSI
- 即插即用 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d86435c2511f539952426b5e2b2c1c8b8a7904a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834933"
---
# <a name="supporting-plug-and-play-in-a-scsi-miniport-driver"></a>支持 SCSI 微型端口驱动程序中的即插即用


## <span id="ddk_supporting_plug_and_play_in_a_scsi_miniport_driver_kg"></span><span id="DDK_SUPPORTING_PLUG_AND_PLAY_IN_A_SCSI_MINIPORT_DRIVER_KG"></span>


尽管 Microsoft Windows 2000 和更高版本的操作系统即插即用操作系统，但默认情况下，SCSI 微型端口驱动程序作为旧驱动程序运行。 旧微型端口驱动程序的 HBA 在运行时无法从系统中删除，也不能在添加到正在运行的系统时自动检测到旧版微型端口驱动程序。 对于某些 Hba，这些限制可能是可接受的，但计算机卡/CardBus Hba 和便携式计算机的 SCSI 微型端口驱动程序应支持即插即用。

即插即用微型端口驱动程序必须实现 *HwScsiAdapterControl* 例程以停止和管理 HBA 的电源。 即插即用微型端口驱动程序不需要任何其他例程来容纳驱动程序初始化中的更改。

SCSI 端口驱动程序为目标设备以及微型端口驱动程序的 FDO 创建 PDOs，并处理请求以代表微型端口驱动程序添加、启动或卸载设备。 有关即插即用驱动程序的常规信息，请参阅 [即插即用](../kernel/introduction-to-plug-and-play.md)。

 

