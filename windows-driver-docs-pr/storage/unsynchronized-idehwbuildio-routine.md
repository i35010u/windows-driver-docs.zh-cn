---
title: 未同步的 IdeHwBuildIo 例程
description: 未同步的 IdeHwBuildIo 例程
ms.assetid: 47e32f05-5c89-4423-b515-c774b94a9b84
keywords:
- ATA 端口驱动程序 WDK，同步
- 同步 WDK ATA 端口驱动程序
- AtaHwBuildIo
- 处理 WDK ATA 端口驱动程序未同步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 907e4cd840ef4f1fd263e0c165f007272a6d9043
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732757"
---
# <a name="unsynchronized-idehwbuildio-routine"></a>未同步的 IdeHwBuildIo 例程


## <span id="ddk_unsynchronized_atahwbuildio_routine_kg"></span><span id="DDK_UNSYNCHRONIZED_ATAHWBUILDIO_ROUTINE_KG"></span>


**注意** ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用 [storport 驱动](./storport-driver-overview.md) 程序和 [storport 微型端口](./storport-miniport-drivers.md) 驱动程序模型。


ATA 端口驱动程序 \_ 会在调用 ATA 微型端口驱动程序的启动 i/o 例程 [**IdeHwStartIo**](/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_startio)之前，将处理器的 IRQL 提高到调度级别或更高级别。 ATA 端口驱动程序会引发处理器的 IRQL 以屏蔽中断，并确保启动 i/o 例程和中断处理程序同步访问关键操作系统结构。 若要减少微型端口驱动程序在 "启动 i/o" 例程的 "IRQL =" 调度级别上花费的时间 &gt; \_ ，微型端口驱动程序提供了 [**IdeHwBuildIo**](/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_buildio) 例程。 ATA 端口驱动程序调用 *IdeHwBuildIo* ，以 irql &lt; = 派单 \_ 级别，使微型端口驱动程序可以在较低的 IRQL 上尽可能多地预处理 i/o 请求，避免对处理器进行独占控制。

Storport i/o 模型使用类似的技术来最大程度地减少启动 i/o 例程所用的时间。 有关 Storport 驱动程序如何使用 [**HwStorBuildIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)的详细信息，请参阅未 [同步的 HwStorBuildIo 例程](unsynchronized-hwstorbuildio-routine.md)。

需要访问关键系统结构（例如设备扩展）的 i/o 请求的所有处理都应在 [**IdeHwStartIo**](/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_startio) 例程内完成。

