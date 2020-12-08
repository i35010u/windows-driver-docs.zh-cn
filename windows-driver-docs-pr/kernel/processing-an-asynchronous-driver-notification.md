---
title: 处理异步驱动程序通知
description: 处理异步驱动程序通知
keywords:
- 驱动程序通知 WDK 动态硬件分区，处理
- 异步驱动程序通知 WDK 动态硬件分区，处理
- 注册驱动程序通知 WDK 动态硬件分区，异步
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39cf63e84b5d76ea2925cf366a831fd4f961e01c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816075"
---
# <a name="processing-an-asynchronous-driver-notification"></a>处理异步驱动程序通知


当操作系统调用注册的回调函数时，它会将指针传递到 *NotificationStructure* 参数中的 [**设备 \_ 接口 \_ 更改 \_ 通知**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_interface_change_notification)结构。

下面的代码示例演示了用于处理处理器的异步驱动程序通知的回调函数的实现：

```cpp
// Asynchronous processor notification callback function
NTSTATUS
  AsyncProcessorCallback(
    IN PVOID NotificationStructure,
    IN PVOID Context
    )
{
  PDEVICE_INTERFACE_CHANGE_NOTIFICATION Notification;
  ULONG ProcessorCount;
  KAFFINITY ActiveProcessors;

  Notification = 
    (PDEVICE_INTERFACE_CHANGE_NOTIFICATION)
      NotificationStructure;

  // Verify that this notification is about a processor
  // that is being added to the hardware partition.
  if (IsEqualGUID(
        &Notification->Event,
        &GUID_DEVICE_INTERFACE_ARRIVAL
        ))
  {
    // Get the current processor count and affinity
    ProcessorCount =
      KeQueryActiveProcessorCount(
        &ActiveProcessors
        );

    // Adjust any resource allocations that are based
    // on the number of processors.
    ...

    // Adjust the assignment of resources that are
    // assigned to specific processors.
    ...

    // Begin scheduling any per processor threads
    // on the new processor.
    ...

    // Adjust the scheduling of DPCs and other threads
    ...

    // Adjust any load balancing algorithms
    ...
  }

  // Always return success status
 return STATUS_SUCCESS;
}
```

下面的代码示例演示了用于处理内存的异步驱动程序通知的回调函数的实现：

```cpp
// Asynchronous memory notification callback function
NTSTATUS
  AsyncMemoryCallback(
    IN PVOID NotificationStructure,
    IN PVOID Context
    )
{
  PDEVICE_INTERFACE_CHANGE_NOTIFICATION Notification;

  Notification = 
    (PDEVICE_INTERFACE_CHANGE_NOTIFICATION)
      NotificationStructure;

  // Verify that this notification is about memory
  // that is being added to the hardware partition.
  if (IsEqualGUID(
        &Notification->Event,
        &GUID_DEVICE_INTERFACE_ARRIVAL
        ))
  {
    // Increase the size of any memory buffers
    // for optimal performance of the driver.
    ...
  }

  // Always return success status
  return STATUS_SUCCESS;
}
```

 

