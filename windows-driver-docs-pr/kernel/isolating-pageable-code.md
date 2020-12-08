---
title: 隔离可分页代码
description: 隔离可分页代码
keywords:
- 可分页驱动程序 WDK 内核，隔离代码
- 隔离可分页代码
- 旋转锁定 WDK 内存
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89c3485240071c76f3e15f1d5ea7d51bcfb536d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801675"
---
# <a name="isolating-pageable-code"></a>隔离可分页代码





无法分页使用旋转锁定的例程。 但是，在某些情况下，你可以将需要自旋锁的操作隔离到一个不会包含在 "可分页" 部分的单独例程中。

例如，请考虑以下代码片段：

```cpp
//  PAGED_CODE(); 
 
KeInitializeEvent( &event, NotificationEvent, FALSE ); 
irp = IoBuildDeviceIoControlRequest( IRP_MJ_DEVICE_CONTROL, 
                                     DeviceObject, 
                                     (PVOID) NULL, 
                                     0, 
                                     (PVOID) NULL, 
                                     0, 
                                     FALSE, 
                                     &event, 
                                     &ioStatus ); 
if (irp) { 
   irpSp = IoGetNextIrpStackLocation( irp ); 
   irpSp->MajorFunction = IRP_MJ_FILE_SYSTEM_CONTROL; 
   irpSp->MinorFunction = IRP_MN_LOAD_FILE_SYSTEM; 
   status = IoCallDriver( DeviceObject, irp ); 
   if (status == STATUS_PENDING) { 
   (VOID) KeWaitForSingleObject( &event, 
                                 Executive, 
                                 KernelMode, 
                                 FALSE, 
                                 (PLARGE_INTEGER) NULL ); 
   } 
} 

SPINLOCKUSE ! 
KeAcquireSpinLock( &IopDatabaseLock, &irql ); 
// Code inside spin lock ...

DeviceObject->ReferenceCount--; 
 
if (!DeviceObject->ReferenceCount && !DeviceObject->AttachedDevice) { 
   //Unload the driver
   .
   .
   . 
} else { 
   KeReleaseSpinLock( &IopDatabaseLock, irql ); 
} 
```

可以通过将引用旋转锁的几行代码移到单独的例程中，使前面的例程可以分页 (节省大约160字节的) 。

此外，请记住，如果驱动程序代码调用任何 **Ke * Xxx*** 支持例程（如 [**KeReleaseMutex**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex) 或 [**KeReleaseSemaphore**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasesemaphore)），其中 *Wait* 参数设置为 **TRUE**，则不得将其标记为可分页。 此类调用在调度级别以 IRQL 返回 \_ 。

 

