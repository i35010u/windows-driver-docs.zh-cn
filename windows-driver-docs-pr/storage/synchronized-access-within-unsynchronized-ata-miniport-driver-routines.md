---
title: ATA 微型端口驱动程序例程内的同步访问
description: 未同步的 ATA 微型端口驱动程序例程中的同步的访问
ms.assetid: ed047579-9f22-4725-a4b0-3c44b8db89ef
keywords:
- ATA 端口驱动程序 WDK，同步
- 同步 WDK ATA 端口驱动程序
- 处理 WDK ATA 端口驱动程序未同步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95aba487a449b86eb18e1be0e67931b719a31feb
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732691"
---
# <a name="synchronized-access-within-ata-miniport-driver-routines"></a>ATA 微型端口驱动程序例程内的同步访问


## <span id="ddk_synchronized_access_within_unsynchronized_ata_miniport_driver_rout"></span><span id="DDK_SYNCHRONIZED_ACCESS_WITHIN_UNSYNCHRONIZED_ATA_MINIPORT_DRIVER_ROUT"></span>


**注意** ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用 [storport 驱动](./storport-driver-overview.md) 程序和 [storport 微型端口](./storport-miniport-drivers.md) 驱动程序模型。


即使 ATA 微型端口驱动程序在其 [**IdeHwBuildIo**](/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_buildio) 例程中不同步处理 i/o 请求，它也可以通过调用 [**AtaPortRequestSynchronizedRoutine**](/windows-hardware/drivers/ddi/irb/nf-irb-ataportrequestsynchronizedroutine)同步对关键系统结构的访问。 此例程类似于 Storport i/o 模型中提供的 [**StorPortSynchronizeAccess**](/windows-hardware/drivers/ddi/storport/nf-storport-storportsynchronizeaccess) 例程。 有关 Storport 微型端口驱动程序如何管理对关键数据结构的同步访问的详细信息，请参阅未同步的 [微型端口驱动程序例程内的同步访问](synchronized-access-within-unsynchronized-miniport-driver-routines.md)。

ATA 微型端口驱动程序调用 **AtaPortRequestSynchronizedRoutine**时，必须提供指向回调例程的指针。 回调例程处理必须与中断处理程序同步的 i/o 请求部分。 为了获得更好的性能，请将驱动程序编写为尽可能少的时间来执行回调例程。

