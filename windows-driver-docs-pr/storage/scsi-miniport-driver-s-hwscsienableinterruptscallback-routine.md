---
title: SCSI 微型端口驱动程序的 HwScsiEnableInterruptsCallback 例程
description: SCSI 微型端口驱动程序的 HwScsiEnableInterruptsCallback 例程
ms.assetid: 8519924f-ad69-46e7-8b24-bf36523f30c9
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiEnableInterruptsCallback
- HwScsiEnableInterruptsCallback
- 中断 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ae7cacfdf81ca220f0ef15ec90b721fb1a3ccf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339933"
---
# <a name="scsi-miniport-drivers-hwscsienableinterruptscallback-routine"></a>SCSI 微型端口驱动程序的 HwScsiEnableInterruptsCallback 例程


## <span id="ddk_scsi_miniport_drivers_hwscsienableinterruptscallback_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIENABLEINTERRUPTSCALLBACK_ROUTINE_KG"></span>


[ **HwScsiEnableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557295)例程完成处理中断驱动 I/O 操作而不禁止在计算机中的其他设备的 I/O 操作。

当*HwScsiEnableInterruptsCallback*例程获取控件，所有系统设备中断都启用除从 HBA 因为*HwScsiInterrupt*例程禁用 HBA 上的中断然后再调用[ **ScsiPortNotification**](https://msdn.microsoft.com/library/windows/hardware/ff564657)。 因此，微型端口驱动程序的*HwScsiInterrupt*例程不能调用并不能干扰有关当前操作时设置的上下文数据*HwScsiEnableInterruptsCallback*例程正在运行。

一个*HwScsiEnableInterruptsCallback*例程应执行以下操作：

1.  使用已设置为导致中断的请求的操作在完成处理的输入的设备扩展中的上下文。

2.  调用**ScsiPortNotification**与*NotificationType * * * RequestComplete** 和只满足 SRB。

3.  调用**ScsiPortNotification**与 * NotificationType ***NextRequest**，或与**NextLuRequest**如果 HBA 支持有标记的队列或每个逻辑的多个请求单位。

4.  调用**ScsiPortNotification**用一个指针指向设备扩展，* NotificationType ***CallDisableInterrupts**，和微型端口驱动程序的*HwScsiDisableInterruptsCallback*例程中, 所述[SCSI 微型端口驱动程序 HwScsiDisableInterruptsCallback 例程](scsi-miniport-driver-s-hwscsidisableinterruptscallback-routine.md)。

5.  返回控件。

基于 NT 的操作系统**ScsiPortNotification**例程调用*HwScsiDisableInterruptsCallback*例程的子集的系统设备中断已禁用。 系统分配硬件优先级 (IRQL) 小于或等于 HBA 的可能没有设备中断。

请参阅[IRQL](https://msdn.microsoft.com/library/windows/hardware/ff551779)有关详细信息。

 

 




