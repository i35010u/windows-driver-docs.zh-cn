---
title: SCSI 微型端口驱动程序的 HwScsiAdapterControl 例程
description: SCSI 微型端口驱动程序的 HwScsiAdapterControl 例程
ms.assetid: ccc5aa02-415d-40d1-a1ed-c7d4d881f4ca
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiAdapterControl
- HwScsiAdapterControl
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b16bc3dd0a92c41a20bd0f60e578f50b0c2cbae
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252459"
---
# <a name="scsi-miniport-drivers-hwscsiadaptercontrol-routine"></a>SCSI 微型端口驱动程序的 HwScsiAdapterControl 例程

## <span id="ddk_scsi_miniport_drivers_hwscsiadaptercontrol_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIADAPTERCONTROL_ROUTINE_KG"></span>

在基于 NT 的操作系统中，如果微型端口[驱动程序不](scsi-miniport-driver-routines.md)支持即插即用，微型端口驱动程序应在[**HW @ no__t-3INITIALIZATION @ no__t-4DATA （scsi）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)中将此入口点设置为**NULL** 。 否则，微型端口驱动程序必须具有[**HwScsiAdapterControl**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85))例程，才能支持其 HBA 的 PnP 和电源管理操作。

在 HBA 已初始化之后但在第一次 i/o 之前，使用**ScsiQuerySupportedControlTypes**的端口驱动程序首先调用微型端口驱动程序的*HwScsiAdapterControl*例程来确定微型端口支持的其他操作驱动器. 微型端口驱动程序在由端口驱动程序分配的受支持 @ no__t-0CONTROL @ no__t-1TYPE @ no__t-2LIST 中设置其支持的操作。 从此初始调用返回*HwScsiAdapterControl*后，端口驱动程序将再次为微型端口驱动程序指示的操作调用例程。

微型端口驱动程序的*HwScsiAdapterControl*例程可以支持以下任意或所有操作：

-   **ScsiStopAdapter**在关闭后关闭 HBA、从系统中删除 HBA，或以其他方式重新配置或禁用 HBA。

    当 SCSI 端口驱动程序调用*HwScsiAdapterControl*停止 HBA 时，它将确保没有未完成的请求。 微型端口驱动程序应禁用 HBA 上的中断，暂停所有处理（包括后台处理不受中断的限制），并使 HBA 处于未初始化状态。 微型端口驱动程序不应释放其资源;如有必要，端口驱动程序将代表微型端口驱动程序释放资源。 此对*HwScsiAdapterControl*的调用前面有一个 SRB @ NO__T-1FUNCTION @ NO__T-2FLUSH 请求，因此不必刷新缓存，除非自刷新请求完成后，其数据已更改。

    对于此 HBA，不会再次调用微型端口驱动程序，直到 PnP 管理器请求重启 HBA，或关闭了电源管理关闭的 HBA。

    请注意，在已从系统中删除 HBA 后，可能会调用*HwScsiAdapterControl*，如任意微型端口驱动程序例程来停止 hba。

-   **ScsiSetBootConfig**还原 HBA 上的任何设置，BIOS 可能需要这些设置才能启动系统。

    如果需要调用[**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata)或[**ScsiPortSetBusDataByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportsetbusdatabyoffset)来还原此类设置，微型端口驱动程序应支持**ScsiSetBootConfig** 。 端口驱动程序在调用例程以停止 HBA 后，使用**ScsiSetBootConfig**调用微型端口驱动程序的*HwScsiAdapterControl* 。

-   **ScsiSetRunningConfig**还原 hba 上的任何设置，在系统运行时，微型端口驱动程序可能需要控制 hba。

    如果需要调用**ScsiPortGetBusData**或[**ScsiPortSetBusDataByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportsetbusdatabyoffset)来还原此类设置，微型端口驱动程序应支持**ScsiSetRunningConfig** 。 端口驱动程序使用**ScsiSetRunningConfig**调用微型端口驱动程序的*HwScsiAdapterControl* ，然后再调用例程来重新启动 HBA。

-   **ScsiRestartAdapter**重新启动已关闭电源管理的 HBA。

    当端口驱动程序调用*HwScsiAdapterControl*来重新启动 HBA 时，以前分配给微型端口驱动程序的所有资源仍然可用，并且其设备扩展和任何逻辑单元扩展都完好无损。 重新启动其 HBA 时，微型端口驱动程序不得调用只能从*HwScsiFindAdapter*调用的例程。

    如果微型端口驱动程序不支持**ScsiRestartAdapter**，则端口驱动程序会调用微型端口驱动程序的*HwScsiFindAdapter*和*HWSCSIINITIALIZE*例程来重新启动 HBA。 但是，此类例程可能会执行重新启动时不必要的检测工作，因此，这种微型端口驱动程序不会像支持**ScsiRestartAdapter**的微型端口驱动程序那样快速启动其 HBA。

有关详细信息，请参阅[**HwScsiAdapterControl**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85)) 。

 

 




