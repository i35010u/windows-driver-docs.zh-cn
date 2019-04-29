---
title: 支持 SCSI 微型端口驱动程序中的即插即用
description: 支持 SCSI 微型端口驱动程序中的即插即用
ms.assetid: c8b148ac-b1ab-4870-8818-5ef1c2d68599
keywords:
- SCSI 微型端口驱动程序 WDK 存储，即插即用
- 即插即用 WDK SCSI
- Plug and Play WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 982e5f875ec298c8c6b2bd1ff0426ee456ba0dc1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366235"
---
# <a name="supporting-plug-and-play-in-a-scsi-miniport-driver"></a>支持 SCSI 微型端口驱动程序中的即插即用


## <span id="ddk_supporting_plug_and_play_in_a_scsi_miniport_driver_kg"></span><span id="DDK_SUPPORTING_PLUG_AND_PLAY_IN_A_SCSI_MINIPORT_DRIVER_KG"></span>


Microsoft Windows 2000 和更高版本操作系统是插操作系统，尽管默认情况下 SCSI 微型端口驱动程序作为运行旧式驱动程序。 虽然它正在运行，也不会自动添加到正在运行的系统时检测到旧的微型端口驱动程序不能从系统中删除旧的微型端口驱动程序的 HBA。 这些限制可能是可接受的某些 Hba，但 SCSI 微型端口驱动程序的 PC 卡/CardBus Hba 和 Hba 在便携式计算机应支持即插。

插微型端口驱动程序必须实现*HwScsiAdapterControl*例程，以停止和管理与 HBA 的能力。 任何其他例程不所需的插微型端口驱动程序，以适应驱动程序初始化中的更改。

SCSI 端口驱动程序创建 PDOs 适用于目标设备和微型端口驱动程序和处理请求 FDO 添加、 启动或代表微型端口驱动程序卸载设备。 有关插驱动程序的常规信息，请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)。

 

 




