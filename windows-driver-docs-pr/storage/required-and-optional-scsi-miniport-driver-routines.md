---
title: 必需的和可选的 SCSI 微型端口驱动程序例程
description: 必需的和可选的 SCSI 微型端口驱动程序例程
ms.assetid: 6fd1f7af-e8ba-4679-bd8c-f757b57821b0
keywords:
- SCSI 微型端口驱动程序 WDK 存储，所需的例程
- SCSI 微型端口驱动程序 WDK 存储，可选的例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27821b58e3fe97dbf8497b07e3292ca002d3e97a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352791"
---
# <a name="required-and-optional-scsi-miniport-driver-routines"></a>必需的和可选的 SCSI 微型端口驱动程序例程

每个 SCSI 微型端口驱动程序必须至少具有以下系统定义的例程：

- [**DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)初始化微型端口驱动程序

- [*HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)来确定在计算机中配置如何 （或是否） 驱动程序支持 HBA(s)

- [*HwScsiInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff557302)来初始化支持的 HBA(s)

- [**HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)启动其 HBA(s) 上侦听传入的请求的操作

- [*HwScsiResetBus* ](https://msdn.microsoft.com/library/windows/hardware/ff557318)处理总线重置请求

根据每个 HBA 和驱动程序设计器，SCSI 微型端口驱动程序还具有某些或所有以下系统定义的例程：

- [**HwScsiInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff557312)对句柄 HBA 生成中断，这是可选的当且仅当 HBA 不会生成中断，因此微型端口驱动程序通过轮询来管理其 HBA 上的所有 I/O 操作。 但是，使用轮询以独占方式有不利影响对微型端口驱动程序的性能和对其 HBA 的 I/O 吞吐量。 这样的微型端口驱动程序还应[ *HwScsiTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff557327)例程。

- [**HwScsiDisableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557288)并[ **HwScsiEnableInterruptsCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff557295)处理延迟 I/O 处理，如果中断驱动 I/O 操作需要很长时间

- *HwScsiTimer*时需要 HBA，或用于由驱动程序设计器的任何其他用途的延迟时间很长的操作。 微型端口驱动程序应具有*HwScsiTimer*例程，如果它没有*HwScsiInterrupt*例程，因此它可以使用*HwScsiTimer*的高效轮询其 HBA 的例程。

- [**HwScsiDmaStarted**](https://msdn.microsoft.com/library/windows/hardware/ff557291)，这是所必需的如果 HBA 使用系统 DMA 控制器，来设置 HBA 传输后已进行系统 DMA 控制器编程端口驱动程序

- [**HwScsiAdapterState**](https://msdn.microsoft.com/library/windows/hardware/ff557278)，这是可选的当且仅当 HBA 具有任何 BIOS 或 x86 实模式驱动程序和/或将永远不会仅限 x86 的 Microsoft Windows 系统中运行

- [**HwScsiAdapterControl**](https://msdn.microsoft.com/library/windows/hardware/ff557274)，这是必需的如果微型端口驱动程序支持即插

每个前面的微型端口驱动程序例程，除[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff552654)，具有来描述其功能所选择的名称。 除**DriverEntry**，这是必需的每个微型端口驱动程序的初始入口点名称，微型端口驱动程序例程的名称可以是驱动程序编写器选择的任何内容。

以下部分介绍的要求和功能的每个微型端口驱动程序例程。

[SCSI 微型端口驱动程序中的错误处理](error-handling-in-scsi-miniport-drivers.md)介绍 SCSI 微型端口驱动程序的错误处理要求。

## <a name="see-also"></a>请参阅

[HwScsiWmiExecuteMethod](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)

[HwScsiWmiFunctionControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)

[HwScsiWmiQueryDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)

[HwScsiWmiQueryReginfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)

[HwScsiWmiSetDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock)

[HwScsiWmiSetDataItem](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)