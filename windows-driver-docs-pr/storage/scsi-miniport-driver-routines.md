---
title: 必需的和可选的 SCSI 微型端口驱动程序例程
description: 必需的和可选的 SCSI 微型端口驱动程序例程
ms.assetid: 6fd1f7af-e8ba-4679-bd8c-f757b57821b0
keywords:
- SCSI 微型端口驱动程序 WDK 存储，必需例程
- SCSI 微型端口驱动程序 WDK 存储，可选例程
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4843e4ae131bbd67d05fb94661190f0927eaab8b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184913"
---
# <a name="required-and-optional-scsi-miniport-driver-routines"></a>必需的和可选的 SCSI 微型端口驱动程序例程

微型端口驱动程序的 *HwScsiXxx* 例程可以具有驱动程序编写器选择的任何名称。 **DriverEntry** 是必需的名称。

每个 SCSI 微型端口驱动程序必须至少具有以下系统定义的例程：

| 所需例程 | 描述 |
| ---------------- | ----------- |
| [**DriverEntry**](driverentry-of-scsi-miniport-driver.md) | 初始化微型端口驱动程序 |
| [*HwScsiFindAdapter*](scsi-miniport-driver-s-hwscsifindadapter-routine.md) | 确定是否在计算机中配置 (或是否) 驱动程序支持的主机总线适配器 (s)  (Hba)  |
| [*HwScsiInitialize*](scsi-miniport-driver-s-hwscsiinitialize-routine.md) | 初始化支持的 HBA ()  |
| [*HwScsiStartIo*](scsi-miniport-driver-s-hwscsistartio-routine.md) | 在微型端口的 HBA 上启动针对传入请求的 (s) 操作 |
| [*HwScsiResetBus*](scsi-miniport-driver-s-hwscsiresetbus-routine.md) | 处理总线重置请求 |

SCSI 微型端口驱动程序还具有以下系统定义的部分或全部，具体取决于每个 HBA 和驱动程序设计器：

|  例程所返回的值 | 描述 |
| -------- | ----------- |
| [*HwScsiInterrupt*](scsi-miniport-driver-s-hwscsiinterrupt-routine.md) | 处理 HBA 生成的中断，当且仅当 HBA 不产生中断时，此操作是可选的，因此，小型端口驱动程序通过轮询管理其 HBA 上的所有 i/o 操作。 但是，仅使用轮询会对微型端口驱动程序的性能及其 HBA 的 i/o 吞吐量产生负面影响。 此类微型端口驱动程序还应具有 [*HwScsiTimer*](scsi-miniport-driver-s-hwscsitimer-routine.md) 例程。 |
| [*HwScsiDisableInterruptsCallback*](scsi-miniport-driver-s-hwscsidisableinterruptscallback-routine.md)和[ *HwScsiEnableInterruptsCallback*](scsi-miniport-driver-s-hwscsienableinterruptscallback-routine.md) | 如果中断驱动的 i/o 操作需要很长时间，请处理延迟的 i/o 处理。 |
| [*HwScsiTimer*](scsi-miniport-driver-s-hwscsitimer-routine.md) | 需要在 HBA 上进行长时间延迟或由驱动程序设计器确定的任何其他目的的时间运算。 如果微型端口驱动程序没有*HwScsiInterrupt*例程，则它应具有*HwScsiTimer*例程，因此它可以使用*HwScsiTimer*例程来有效地轮询其 HBA。 |
| [*HwScsiDmaStarted*](scsi-miniport-driver-s-hwscsidmastarted-routine.md) | 如果 HBA 使用系统 DMA 控制器，则需要在端口驱动程序对系统 DMA 控制器进行编程后设置 HBA 传输。 |
| [*HwScsiAdapterState*](scsi-miniport-driver-s-hwscsiadapterstate-routine.md) | 当且仅当 HBA 没有 BIOS 或 x86-实模式驱动程序和/或从不在仅 x86 的 Microsoft Windows 系统中运行时，可选。 |
| [*HwScsiAdapterControl*](scsi-miniport-driver-s-hwscsiadaptercontrol-routine.md) | 如果微型端口驱动程序支持即插即用，则为必需。 |
| [HwScsiWmiExecuteMethod](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method) | 执行与数据块关联的方法。 此例程是可选的。 |
| [HwScsiWmiFunctionControl](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_function_control) | 启用或禁用事件通知，同时启用或禁用对小型端口驱动程序所指定为收集开销较高的数据块的数据收集。 可选。 |
| [HwScsiWmiQueryDataBlock](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock) | 获取数据块的单个实例或所有实例。 必需。 |
| [HwScsiWmiQueryReginfo](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo) | 获取要通过 SCSI 端口驱动程序代表微型端口驱动程序注册的数据和事件块的相关信息。 必需。 |
| [HwScsiWmiSetDataBlock](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock) | 更改数据块的单个实例中的所有数据项。 可选。 |
| [HwScsiWmiSetDataItem](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem) | 更改数据块的实例中的单个数据项。 可选。 |

上述每个小型小型驱动程序例程（ [**DriverEntry**](driverentry-of-scsi-miniport-driver.md)除外）都有一个用于描述其功能的名称。 除了 **DriverEntry**（这是每个微型端口驱动程序的初始入口点所需的名称），小型端口驱动程序例程的名称可以是驱动程序编写器选择的任何内容。

[Scsi 微型端口驱动程序中的错误处理](error-handling-in-scsi-miniport-drivers.md) 介绍了 scsi 微型端口驱动程序的错误处理要求。