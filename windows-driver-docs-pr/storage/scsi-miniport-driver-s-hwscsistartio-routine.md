---
title: SCSI 微型端口驱动程序的 HwScsiStartIo 例程
description: SCSI 微型端口驱动程序的 HwScsiStartIo 例程
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- 传入 i/o 请求 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 886859b5ace43e17a242ceb252c2aa5004559244
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828383"
---
# <a name="scsi-miniport-drivers-hwscsistartio-routine"></a>SCSI 微型端口驱动程序的 HwScsiStartIo 例程


## <span id="ddk_scsi_miniport_drivers_hwscsistartio_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSISTARTIO_ROUTINE_KG"></span>


顾名思义， [**HwScsiStartIo**](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85)) 例程是对 HBA 驱动总线上的外围设备的传入请求的入口点， (es) 。 使用指向 SCSI 请求块 (SRB) 的指针和针对每 HBA 状态的微型端口驱动程序的设备扩展调用 *HwScsiStartIo* 。 有关此例程的语法的信息，请参阅 **HwScsiStartIo**。

如果微型端口驱动程序的 **DriverEntry** 例程还请求为逻辑单元扩展分配内存 (参阅 [调用 ScsiPortInitialize](calling-scsiportinitialize.md)) ，则 *HwScsiStartIo* 例程会调用 **ScsiPortGetLogicalUnit** ，其中包含输入设备扩展指针以及输入 PathId 中的 **TargetId**、 **SRB** 和 **Lun** 值。

如果 **DriverEntry** 例程请求为 SRB 扩展分配内存，则每个 SRB 中的 **SrbExtension** 成员将包含一个指向微型端口驱动程序的每个请求存储区域的指针。 请注意，微型端口驱动程序必须请求为 **SrbExtension** 分配内存（如果它保留每个请求的状态信息）。 不能使用 SRB 来实现此目的。

 

