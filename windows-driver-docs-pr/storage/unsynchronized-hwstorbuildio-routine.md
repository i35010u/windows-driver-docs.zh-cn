---
title: 未同步的 HwStorBuildIo 例程
description: 未同步的 HwStorBuildIo 例程
ms.assetid: 6b18e3ff-30dd-414b-99b5-4bb914660a67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34868e3dcd7212753478ddd6daaaf7fbae08ba28
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186637"
---
# <a name="unsynchronized-hwstorbuildio-routine"></a>未同步的 HwStorBuildIo 例程


## <span id="ddk_unsynchronized_hwstorbuildio_routine_kg"></span><span id="DDK_UNSYNCHRONIZED_HWSTORBUILDIO_ROUTINE_KG"></span>


在 SCSI 端口-微型端口驱动程序 i/o 模型中，微型端口驱动程序的 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程 [**HwScsiStartIo**](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))应该尽快将 SCSI 请求块传输 () SRBs 硬件。 这一点非常重要，因为在微型端口驱动程序的 *StartIo* 例程中完成的工作是在禁用了中断并且在 IRQL = 调度级别进行的 \_ 。 遗憾的是，此模型不适合 (Hba) 的某些高性能主机总线适配器的驱动程序，因为在启动 i/o 时，这些 Hba 的微型端口驱动程序必须执行大量的处理。 如果微型端口驱动程序在其 *StartIo* 例程中进行此处理，则会降低系统性能。

Storport i/o 模型支持 [**HwStorBuildIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio) 例程，努力消除微型端口驱动程序的 *StartIo* 例程 [**HwStorStartIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)中的一些处理负担。 在 Storport i/o 模型中，系统刚好在调用微型端口驱动程序的*HwStorStartIo*例程之前调用*HwStorBuildIo* ，并尽可能多地进行处理。 此策略可避免争用 CPU 周期和访问关键系统结构（例如设备扩展），因为 *HwStorBuildIo* 以较低的 IRQL 执行并且不保留任何同步锁。

*HwStorBuildIo*例程应将 SRB 转换为更方便的数据结构，生成散点/集合列表，并执行其他每个 SRB 处理。 由于在 *HwStorBuildIo* 例程执行期间不会持有任何锁，因此微型端口驱动程序不应访问 SRB 和 SRB 扩展中的任何其他数据。 如果在处理过程中需要访问其他结构，则仍应在 *HwStartIo* 例程中执行该部分。

若要实现最大性能，应将 *HwStorBuildIo* 例程与全双工模式结合使用。

 

