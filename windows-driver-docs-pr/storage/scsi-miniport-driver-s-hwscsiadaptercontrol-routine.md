---
title: SCSI 微型端口驱动程序的 HwScsiAdapterControl 例程
description: SCSI 微型端口驱动程序的 HwScsiAdapterControl 例程
ms.assetid: ccc5aa02-415d-40d1-a1ed-c7d4d881f4ca
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiAdapterControl
- HwScsiAdapterControl
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2034a3919e09ecbfb462c801a25ade9aa47220cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520865"
---
# <a name="scsi-miniport-drivers-hwscsiadaptercontrol-routine"></a>SCSI 微型端口驱动程序的 HwScsiAdapterControl 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiadaptercontrol_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIADAPTERCONTROL_ROUTINE_KG"></span>


在基于 NT 的操作系统，微型端口驱动程序应将此入口点设置为**NULL**中[ **HW\_初始化\_数据 (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff557456) (请参阅[必需和可选 SCSI 微型端口驱动程序例程](required-and-optional-scsi-miniport-driver-routines.md)) 如果微型端口驱动程序不支持即插。 否则，微型端口驱动程序必须具有[ **HwScsiAdapterControl**](https://msdn.microsoft.com/library/windows/hardware/ff557274)例程以支持其 HBA 的 PnP 和电源管理操作。

微型端口驱动程序*HwScsiAdapterControl*端口驱动程序与第一次调用例程**ScsiQuerySupportedControlTypes** HBA 初始化后但在第一次 I/O，以确定之前微型端口驱动程序支持的其他操作。 微型端口驱动程序设置支持中受支持的操作数\_控制\_类型\_分配的端口驱动程序的列表。 之后*HwScsiAdapterControl*端口驱动程序仅为指示的微型端口驱动程序调用例程再次从该初始调用时，返回。

微型端口驱动程序*HwScsiAdapterControl*例程可以支持任何或所有以下操作：

-   **ScsiStopAdapter**关闭 HBA 时它已关机，从系统中删除或否则为重新配置的或已禁用。

    SCSI 端口驱动程序时调用*HwScsiAdapterControl*若要停止 HBA，它确保没有任何未完成的请求。 微型端口驱动程序应禁用 HBA 上的中断、 暂停包括后台处理不受中断影响的所有处理并放入未初始化状态的 HBA。 微型端口驱动程序不应释放其资源;如有必要，端口驱动程序将代表微型端口驱动程序释放资源。 此调用*HwScsiAdapterControl* SRB 前面\_函数\_刷新请求，因此不需要刷新缓存，除非其数据发生更改，因为刷新请求已完成。

    微型端口驱动程序不会再调用此 hba 直到 PnP 管理器请求，HBA 重新启动，或接通电源管理的已关闭的 HBA。

    请注意， *HwScsiAdapterControl*，像任何微型端口驱动程序例程，可能会调用后已从系统中删除了 HBA 停止 HBA。

-   **ScsiSetBootConfig**还原 BIOS 可能需要启动系统的 HBA 上的任何设置。

    微型端口驱动程序应支持**ScsiSetBootConfig**如果它需要调用[ **ScsiPortGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff564624)或者[ **ScsiPortSetBusDataByOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff564751)还原此类设置。 端口驱动程序调用微型端口驱动程序*HwScsiAdapterControl*与**ScsiSetBootConfig**后调用的例程来停止 HBA。

-   **ScsiSetRunningConfig**还原微型端口驱动程序可能需要在系统运行时控制 HBA 的 HBA 上的任何设置。

    微型端口驱动程序应支持**ScsiSetRunningConfig**如果它需要调用**ScsiPortGetBusData**或[ **ScsiPortSetBusDataByOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff564751)若要还原此类设置。 端口驱动程序调用微型端口驱动程序*HwScsiAdapterControl*与**ScsiSetRunningConfig**之前调用重启 HBA 的例程。

-   **ScsiRestartAdapter**重新启动已关闭电源管理的 HBA。

    在时间端口驱动程序调用*HwScsiAdapterControl*重启 HBA，以前分配给微型端口驱动程序的所有资源都都仍然可用并且其设备扩展的任何逻辑单元扩展保持都不变。 当重新启动其的 HBA，微型端口驱动程序不能调用只能从调用的例程*HwScsiFindAdapter*。

    如果微型端口驱动程序不支持**ScsiRestartAdapter**，端口驱动程序调用微型端口驱动程序*HwScsiFindAdapter*并*HwScsiInitialize*例程重新启动 HBA。 但是，此类例程可能会执行的是不必要时重新启动，因此这样的微型端口驱动程序将不会接通其 HBA 作为支持的微型端口驱动程序快速检测工作**ScsiRestartAdapter**。

请参阅[ **HwScsiAdapterControl** ](https://msdn.microsoft.com/library/windows/hardware/ff557274)有关详细信息。

 

 




