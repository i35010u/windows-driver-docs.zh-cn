---
title: 重复使用 IRP
description: 重复使用 IRP
keywords:
- Irp WDK 内核，重复使用
- 重用 Irp WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42a213453c04fcf0d2fbe8b6afed11b5bca1f910
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834425"
---
# <a name="reusing-irps"></a>重复使用 IRP





在某些情况下，驱动程序可以 *重复使用* irp。 驱动程序可以分配用于保存 Irp 的内存缓冲区池，因为需要创建它们。

驱动程序不得尝试重用由 i/o 管理器发出的 Irp。 具体而言，驱动程序不应尝试重复使用由 [**IoMakeAssociatedIrp**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp)、 [**IoBuildSynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)、 [**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)或 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 例程创建的 irp。

驱动程序可以安全地重用已创建的 Irp，如下所示：

1.  如果驱动程序将 IRP 分配为原始内存 (例如，通过调用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)) ，然后使用 [**IoInitializeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp)对其进行初始化，则可以安全地调用 **IoInitializeIrp** 或 [**IoReuseIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp) 来重新初始化内存缓冲区。

2.  在 Microsoft Windows 2000 及更高版本的操作系统上，使用 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 创建 irp 的驱动程序可以通过调用 **IOREUSEIRP** 重复使用 irp。

3.  如果驱动程序通过调用 **IoAllocateIrp** 来分配 irp，并将 *ChargeQuota* 参数设置为 **FALSE**，则可以安全地使用 **IoInitializeIrp** 重新初始化 irp。 必须在 Windows 98/Me 上工作的驱动程序可以使用此方法解决。 严格适用于 Windows 2000 和更高版本操作系统的驱动程序应使用上述方法。

 

