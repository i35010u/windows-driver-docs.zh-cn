---
title: 未同步的 HwStorBuildIo 例程
description: 未同步的 HwStorBuildIo 例程
ms.assetid: 6b18e3ff-30dd-414b-99b5-4bb914660a67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a09fe0e96910027c62ce0ed76fa75a65ce4da90
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390205"
---
# <a name="unsynchronized-hwstorbuildio-routine"></a>未同步的 HwStorBuildIo 例程


## <span id="ddk_unsynchronized_hwstorbuildio_routine_kg"></span><span id="DDK_UNSYNCHRONIZED_HWSTORBUILDIO_ROUTINE_KG"></span>


在 SCSI 端口的微型端口驱动程序 I/O 模型，微型端口驱动程序[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程[ **HwScsiStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff557323)，应传输 SCSI尽可能快地请求块 (Srb) 的硬件。 这是必要的因为微型端口驱动程序中完成工作*StartIo*例程完成时中断处于禁用状态和在 IRQL = 调度\_级别。 遗憾的是，此模型不适合于驱动程序的某些高效的主机总线适配器 (Hba)，因为启动 I/O 时，这些 Hba 的微型端口驱动程序必须执行大量的处理。 如果微型端口驱动程序执行此处理其*StartIo*例程，则它会降低系统性能。

Storport I/O 模型支持[ **HwStorBuildIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557369)例程中为了从微型端口驱动程序中删除的一些处理负担*StartIo*例程， [**HwStorStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff557423)。 在 Storport I/O 模型中，系统会调用*HwStorBuildIo*只需在调用微型端口驱动程序之前先*HwStorStartIo*例程并尽可能处理为可能存在。 此策略可以避免争用 CPU 周期和对关键系统结构，例如设备扩展的访问，因为*HwStorBuildIo*在较低的 IRQL 执行，并不持有的任何同步锁。

*HwStorBuildIo*例程应转换到更方便的数据结构 SRB，生成散播-聚集列表，并执行其他每个 SRB 处理操作。 因为在执行期间不持有任何锁*HwStorBuildIo*例程，微型端口驱动程序应访问 SRB 和 SRB 扩展以外的任何数据。 如果需要处理的过程中对其他结构的访问，则在该部分，仍应在执行*HwStartIo*例程。

若要实现最大性能*HwStorBuildIo*例程应与全双工模式结合使用。

 

 




