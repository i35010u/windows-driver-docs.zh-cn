---
title: 隔离可分页代码
description: 隔离可分页代码
ms.assetid: 86189154-606a-4df8-b3a9-040bbaffaa2f
keywords:
- 可分页的驱动程序 WDK 内核，隔离代码
- 隔离可分页的代码
- 数值调节钮锁 WDK 内存
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 056257ab3c5f732f5703d2acab3800ed4cada192
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376437"
---
# <a name="isolating-pageable-code"></a>隔离可分页代码





不能分页使用旋转锁的例程。 但是，在某些情况下可以隔离需要旋转锁不会包含在可分页部分的单独例程中的操作。

例如，考虑以下片段：

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

前面的例程不能建立可分页 （节省大约 160 个字节） 通过将移动到一个单独的例程引用旋转锁几行代码。

此外，请记住，驱动程序代码不能标记为可分页，如果它调用任何**Ke * Xxx*** 支持例程，如[ **KeReleaseMutex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasemutex)或[ **KeReleaseSemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasesemaphore)，在其中*等待*参数设置为**TRUE**。 此类调用将返回具有在调度的 IRQL\_级别。

 

 




