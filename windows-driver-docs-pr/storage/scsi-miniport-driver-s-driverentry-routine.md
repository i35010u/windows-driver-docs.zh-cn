---
title: SCSI 微型端口驱动程序的 DriverEntry 例程
description: SCSI 微型端口驱动程序的 DriverEntry 例程
ms.assetid: b143bb19-2c9e-4e43-841f-a3c47c7f1a1b
keywords:
- DriverEntry WDK 存储
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5eba3fdcc63b2efe61b6a69ce76db741f0461bfe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842680"
---
# <a name="scsi-miniport-drivers-driverentry-routine"></a>SCSI 微型端口驱动程序的 DriverEntry 例程

**DriverEntry**例程是大多数 Microsoft Windows 内核模式驱动程序和每个 SCSI 微型端口驱动程序的初始入口点。 使用 PVOID 类型的两个输入参数调用微型端口驱动程序的[**DriverEntry**](driverentry-of-scsi-miniport-driver.md)例程，并且必须执行以下操作：

1. 使用零初始化堆栈上的[HW_INITIALIZATION_DATA （SCSI）](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)结构。

2. 将**HwInitializationDataSize**成员设置为**sizeof**（HW_INITIALIZATION_DATA）。

3. 在 HW_INITIALIZATION_DATA 成员中设置特定于驱动程序和特定于 HBA 的值，包括微型端口驱动程序的入口点。 必须设置以下入口点：

   - [*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))
   - [*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))
   - [*HwScsiStartIo*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))
   - [*HwScsiResetBus*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))

    以下入口点可以设置为驱动程序提供的例程，也可以设置为**NULL**：

  - [*HwScsiInterrupt*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85)) （如果微型端口驱动程序只使用轮询，则**为 NULL** ）
  - [*HwScsiDmaStarted*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557291(v=vs.85)) （如果 HBA 使用 PIO 或总线主机，则**为 NULL** ）
  - [*HwScsiAdapterState*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85)) （**如果**微型端口驱动程序仅在基于 NT 的操作系统平台上运行，或者它设计为也在仅 x86 Windows 平台上运行，但 HBA 既无 BIOS 也没有 x86 纯模式驱动程序）
  - [*HwScsiAdapterControl*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85)) （如果微型端口驱动程序不支持即插即用，则**为 NULL** ）

4. 在旧式微型端口驱动程序中，设置任何驱动程序确定的、微型端口驱动程序的*HwScsiFindAdapter*例程将使用的上下文数据。

5. 调用[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize) ，并在**DriverEntry**例程中输入的指针、已填充 HW_INITIALIZATION_DATA 的地址和上下文数据的地址（如果有）。
