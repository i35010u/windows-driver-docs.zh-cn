---
title: SCSI 微型端口驱动程序的 DriverEntry 例程
description: SCSI 微型端口驱动程序的 DriverEntry 例程
ms.assetid: b143bb19-2c9e-4e43-841f-a3c47c7f1a1b
keywords:
- DriverEntry WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44deea792e1c57be7eb912ee6e7a83602962f950
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384332"
---
# <a name="scsi-miniport-drivers-driverentry-routine"></a>SCSI 微型端口驱动程序的 DriverEntry 例程


## <span id="ddk_scsi_miniport_drivers_driverentry_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


一个[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)例程是大多数 Microsoft Windows NT 内核模式驱动程序和每个 SCSI 微型端口驱动程序的初始入口点。 微型端口驱动程序**DriverEntry**例程称为类型 PVOID 的两个输入参数，必须执行以下操作：

1.  初始化[ **HW\_初始化\_数据 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)用零堆栈上的结构。

2.  设置**HwInitializationDataSize**成员添加到**sizeof**(HW\_初始化\_数据)。

3.  在硬件中设置特定于驱动程序和特定于 HBA 的值\_初始化\_数据成员，包括微型端口驱动程序的入口点。 必须设置以下入口点：

    -   [*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))
    -   [*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))
    -   [**HwScsiStartIo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))
    -   [*HwScsiResetBus*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))

    以下入口点可以设置为驱动程序提供的例程，或者必须设置为**NULL**:

    -   [**HwScsiInterrupt** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557312(v=vs.85)) (**NULL**如果微型端口驱动程序将使用轮询以独占方式)
    -   [**HwScsiDmaStarted** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557291(v=vs.85)) (**NULL**如果 HBA 使用 PIO 或是总线母版)
    -   [**HwScsiAdapterState** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85)) (**NULL**如果微型端口驱动程序只能在基于 NT 的操作系统平台上运行或如果它设计还为在仅限 x86 的 Windows 平台上运行，但 HBA 都不是 BIOS，也不x86 实模式驱动程序）
    -   [**HwScsiAdapterControl** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85)) (**NULL**微型端口驱动程序不支持即插)

4.  在旧的微型端口驱动程序，设置的任何驱动程序确定上下文数据的微型端口驱动程序*HwScsiFindAdapter*例程将使用。

5.  调用[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)与输入到指针**DriverEntry**例程，已填写的 HW 地址\_初始化\_数据和上下文数据，如果有的地址。

 

 




