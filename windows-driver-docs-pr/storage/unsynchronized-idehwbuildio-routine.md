---
title: 未同步的 IdeHwBuildIo 例程
description: 未同步的 IdeHwBuildIo 例程
ms.assetid: 47e32f05-5c89-4423-b515-c774b94a9b84
keywords:
- ATA 端口驱动程序 WDK，同步
- 同步 WDK ATA 端口驱动程序
- AtaHwBuildIo
- 未同步的处理 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2240bc7e14449a323effff916b5e399f5a7ebad0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386809"
---
# <a name="unsynchronized-idehwbuildio-routine"></a>未同步的 IdeHwBuildIo 例程


## <span id="ddk_unsynchronized_atahwbuildio_routine_kg"></span><span id="DDK_UNSYNCHRONIZED_ATAHWBUILDIO_ROUTINE_KG"></span>


**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。


ATA 端口驱动程序引发调度到处理器的 IRQL\_级别或上述调用之前 ATA 微型端口驱动程序的启动 I/O 例程[ **IdeHwStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_startio)。 ATA 端口驱动程序会引发处理器 IRQL，若要屏蔽的中断出，并保证开始 I/O 例程和中断处理程序同步对关键的操作系统结构的访问。 若要减少微型端口驱动程序在启动 I/O 例程在 IRQL 中花费的时间&gt;= 调度\_级别、 微型端口驱动程序提供[ **IdeHwBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_buildio)例程。 ATA 端口驱动程序调用*IdeHwBuildIo*在 IRQL &lt;= 调度\_级别，以便微型端口驱动程序可以在较低的 IRQL 尽可能预处理尽可能多的 I/O 请求并避免独占的控制处理器。

Storport I/O 模型使用了类似的方法来最大程度减少在其开始 I/O 例程中所用的时间。 有关如何使用 Storport 驱动程序详细信息[ **HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)，请参阅[未同步 HwStorBuildIo 例程](unsynchronized-hwstorbuildio-routine.md)。

应中完成所有处理 I/O 请求需要访问关键系统结构，例如设备扩展[ **IdeHwStartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_startio)例程。

 

 


