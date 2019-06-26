---
title: 必需的和可选的 SCSI 微型端口驱动程序例程
description: 必需的和可选的 SCSI 微型端口驱动程序例程
ms.assetid: 6fd1f7af-e8ba-4679-bd8c-f757b57821b0
keywords:
- SCSI 微型端口驱动程序 WDK 存储，所需的例程
- SCSI 微型端口驱动程序 WDK 存储，可选的例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6f39a12a5f6d5d0951284a6dbe17dcac39a4998
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368895"
---
# <a name="required-and-optional-scsi-miniport-driver-routines"></a>必需的和可选的 SCSI 微型端口驱动程序例程

每个 SCSI 微型端口驱动程序必须至少具有以下系统定义的例程：

- [**DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)初始化微型端口驱动程序

- [*HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))来确定在计算机中配置如何 （或是否） 驱动程序支持 HBA(s)

- [*HwScsiInitialize* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))来初始化支持的 HBA(s)

- [**HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))启动其 HBA(s) 上侦听传入的请求的操作

- [*HwScsiResetBus* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))处理总线重置请求

根据每个 HBA 和驱动程序设计器，SCSI 微型端口驱动程序还具有某些或所有以下系统定义的例程：

- [**HwScsiInterrupt**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85))对句柄 HBA 生成中断，这是可选的当且仅当 HBA 不会生成中断，因此微型端口驱动程序通过轮询来管理其 HBA 上的所有 I/O 操作。 但是，使用轮询以独占方式有不利影响对微型端口驱动程序的性能和对其 HBA 的 I/O 吞吐量。 这样的微型端口驱动程序还应[ *HwScsiTimer* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557327(v=vs.85))例程。

- [**HwScsiDisableInterruptsCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557288(v=vs.85))并[ **HwScsiEnableInterruptsCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557295(v=vs.85))处理延迟 I/O 处理，如果中断驱动 I/O 操作需要很长时间

- *HwScsiTimer*时需要 HBA，或用于由驱动程序设计器的任何其他用途的延迟时间很长的操作。 微型端口驱动程序应具有*HwScsiTimer*例程，如果它没有*HwScsiInterrupt*例程，因此它可以使用*HwScsiTimer*的高效轮询其 HBA 的例程。

- [**HwScsiDmaStarted**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557291(v=vs.85))，这是所必需的如果 HBA 使用系统 DMA 控制器，来设置 HBA 传输后已进行系统 DMA 控制器编程端口驱动程序

- [**HwScsiAdapterState**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85))，这是可选的当且仅当 HBA 具有任何 BIOS 或 x86 实模式驱动程序和/或将永远不会仅限 x86 的 Microsoft Windows 系统中运行

- [**HwScsiAdapterControl**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85))，这是必需的如果微型端口驱动程序支持即插

每个前面的微型端口驱动程序例程，除[ **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，具有来描述其功能所选择的名称。 除**DriverEntry**，这是必需的每个微型端口驱动程序的初始入口点名称，微型端口驱动程序例程的名称可以是驱动程序编写器选择的任何内容。

以下部分介绍的要求和功能的每个微型端口驱动程序例程。

[SCSI 微型端口驱动程序中的错误处理](error-handling-in-scsi-miniport-drivers.md)介绍 SCSI 微型端口驱动程序的错误处理要求。

## <a name="see-also"></a>请参阅

[HwScsiWmiExecuteMethod](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)

[HwScsiWmiFunctionControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)

[HwScsiWmiQueryDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)

[HwScsiWmiQueryReginfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)

[HwScsiWmiSetDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock)

[HwScsiWmiSetDataItem](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)