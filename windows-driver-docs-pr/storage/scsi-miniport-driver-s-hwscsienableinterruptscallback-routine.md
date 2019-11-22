---
title: SCSI 微型端口驱动程序的 HwScsiEnableInterruptsCallback 例程
description: SCSI 微型端口驱动程序的 HwScsiEnableInterruptsCallback 例程
ms.assetid: 8519924f-ad69-46e7-8b24-bf36523f30c9
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiEnableInterruptsCallback
- HwScsiEnableInterruptsCallback
- 中断 WDK SCSI
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 87159bbebfd343e7f285a7b383527b87ddef593e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842673"
---
# <a name="scsi-miniport-drivers-hwscsienableinterruptscallback-routine"></a>SCSI 微型端口驱动程序的 HwScsiEnableInterruptsCallback 例程

对于计算机中的其他设备， [*HwScsiEnableInterruptsCallback*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557295(v=vs.85))例程处理中断驱动的 i/o 操作，而不执行抑制 i/o 操作。

当*HwScsiEnableInterruptsCallback*例程获得控制时，除了 hba 外，还会启用所有系统设备中断，因为*HwScsiInterrupt*例程会在其调用[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)之前禁用 hba 中断。 因此，当*HwScsiEnableInterruptsCallback*例程正在运行时，不能调用微型端口驱动程序的*HwScsiInterrupt*例程，也不能干扰它为当前操作设置的上下文数据。

*HwScsiEnableInterruptsCallback*例程应执行以下操作：

1. 使用在输入设备扩展中为操作设置的上下文来完成导致中断的请求的处理。

2. 与*NotificationType * * * RequestComplete** 和**ScsiPortNotification**的 SRB 一起调用。

3. 如果 HBA 支持标记队列或每个逻辑单元多个请求，请将**ScsiPortNotification**与 * NotificationType ***NextRequest**或 with **NextLuRequest**一起调用。

4. 调用**ScsiPortNotification** ，其中包含指向设备扩展、* NotificationType ***CallDisableInterrupts**和微型端口驱动程序的*HwScsiDisableInterruptsCallback*例程（如[SCSI 微型端口驱动程序的HwScsiDisableInterruptsCallback 例程](scsi-miniport-driver-s-hwscsidisableinterruptscallback-routine.md)。

5. 返回控件。

基于 NT 的操作系统**ScsiPortNotification**例程会调用*HwScsiDisableInterruptsCallback*例程，并禁用部分系统设备中断。 如果系统分配的硬件优先级（IRQL）小于或等于 HBA，则不会出现任何设备中断。

有关详细信息，请参阅[管理硬件优先级](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities
)。
