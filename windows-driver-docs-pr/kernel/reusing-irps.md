---
title: 重复使用 IRP
description: 重复使用 IRP
ms.assetid: 19b09cf8-b88d-4808-9af0-038d3d02dceb
keywords:
- Irp WDK 内核，重复使用
- 重用 Irp WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b75e052efd478013ff5d3c532e481ae1250acf0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838447"
---
# <a name="reusing-irps"></a>重复使用 IRP





在某些情况下，驱动程序可以*重复使用*irp。 驱动程序可以分配用于保存 Irp 的内存缓冲区池，因为需要创建它们。

驱动程序不得尝试重用由 i/o 管理器发出的 Irp。 具体而言，驱动程序不应尝试重复使用由[**IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp)、 [**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)、 [**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)或[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)例程创建的 irp。

驱动程序可以安全地重用已创建的 Irp，如下所示：

1.  如果驱动程序将 IRP 分配为原始内存（例如，通过调用[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)），然后使用[**IoInitializeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp)对其进行初始化，则可以安全地调用**IoInitializeIrp**或[**IoReuseIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)来重新初始化内存宽限.

2.  在 Microsoft Windows 2000 及更高版本的操作系统上，使用[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)创建 irp 的驱动程序可以通过调用**IOREUSEIRP**重复使用 irp。

3.  如果驱动程序通过调用**IoAllocateIrp**来分配 irp，并将*ChargeQuota*参数设置为**FALSE**，则可以安全地使用**IoInitializeIrp**重新初始化 irp。 必须在 Windows 98/Me 上工作的驱动程序可以使用此方法解决。 严格适用于 Windows 2000 和更高版本操作系统的驱动程序应使用上述方法。

 

 




