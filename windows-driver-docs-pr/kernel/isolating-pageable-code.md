---
title: 隔离可分页代码
description: 隔离可分页代码
ms.assetid: 86189154-606a-4df8-b3a9-040bbaffaa2f
keywords:
- 可分页驱动程序 WDK 内核，隔离代码
- 隔离可分页代码
- 旋转锁定 WDK 内存
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 406319d3b82b11288d89c10ccf7a070090d3769d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827923"
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

通过将引用旋转锁的几行代码移到单独的例程中，可以对上述例程进行分页（节省大约160个字节）。

此外，请记住，如果驱动程序代码调用任何**Ke * Xxx*** 支持例程（如[**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)或[**KeReleaseSemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasesemaphore)），其中*Wait*参数设置为**TRUE**，则不得将其标记为可分页。 此类调用在调度\_级别上以 IRQL 返回。

 

 




