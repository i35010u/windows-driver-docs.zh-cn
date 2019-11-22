---
title: 无法检查驱动程序的状态
description: 无法检查驱动程序的状态
ms.assetid: 963f79f6-2282-41bd-9cf4-bd5bc02a510e
keywords:
- reliability WDK kernel , driver state checking
- checking driver states
- driver state checking
- verifying driver states
- correct device states WDK kernel
- device states WDK kernel
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2f67b5b97a2eae9fdba1545fd1c6586cc25b8c6
ms.sourcegitcommit: 01bcf26722f1a51d2b5ebcdcbc08518b3ee08474
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74308543"
---
# <a name="failure-to-check-a-drivers-state"></a>无法检查驱动程序的状态





In the following example, the driver uses the **ASSERT** macro to check for the correct device state in a debug version of a driver image, but does not check device state in the retail build of the same driver source:

```cpp
   case IOCTL_WAIT_FOR_EVENT:

      ASSERT((!Extension->WaitEventIrp));
      Extension->WaitEventIrp = Irp;
      IoMarkIrpPending(Irp);
      status = STATUS_PENDING;
```

In the debug driver image, if the driver already holds the IRP pending, the system will assert. In a retail build, however, the driver does not check for this error. Two calls to the same IOCTL cause the driver to lose track of an IRP.

On a multiprocessor system, this code fragment might cause additional problems. Assume that on entry this routine has ownership of (the right to manipulate) this IRP. When the routine saves the **Irp** pointer in the global structure at **Extension-&gt;WaitEventIrp**, another thread can get the IRP address from that global structure and perform operations on the IRP. To prevent this problem, the driver should mark the IRP pending before it saves the IRP and should include both the call to [**IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) and the assignment in an interlocked sequence. A [*Cancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) routine for the IRP might also be necessary.

 

 




