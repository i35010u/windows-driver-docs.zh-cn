---
title: 注册异步驱动程序通知
description: 注册异步驱动程序通知
ms.assetid: e1f97a65-7c82-4d7b-97ec-0293fc69fd8c
keywords:
- 驱动程序通知 WDK 动态硬件分区，注册
- 异步通知 WDK 动态硬件分区
- 通知 WDK 动态硬件分区，注册
- 异步驱动程序通知 WDK 动态硬件分区，注册
- 注册驱动程序通知 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4424256fd4d534e34452083c47d42fe5f8a52a24
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187739"
---
# <a name="registering-for-asynchronous-driver-notification"></a>注册异步驱动程序通知


若要使用异步驱动程序通知，设备驱动程序可实现在将处理器或内存模块动态添加到硬件分区时操作系统调用的回调函数。 下面的代码示例显示了此类回调函数的原型：

```cpp
// Prototypes for the asynchronous
// notification callback functions
NTSTATUS
  AsyncProcessorCallback(
    IN PVOID NotificationStructure,
    IN PVOID Context
    );

NTSTATUS
  AsyncMemoryCallback(
    IN PVOID NotificationStructure,
    IN PVOID Context
    );
```

设备驱动程序通过对每个设备驱动程序的回调函数调用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification) 函数来注册异步通知，同时为 *EventCategoryData* 参数指定一个指向以下 guid 的指针：

<a href="" id="guid-device-processor"></a>GUID \_ 设备 \_ 处理器  
注册以便在将处理器动态添加到硬件分区时获得通知。

<a href="" id="guid-device-memory"></a>GUID \_ 设备 \_ 内存  
注册以在将内存动态添加到硬件分区时收到通知。

这些 Guid 在头文件 Poclass 中定义。

下面的代码示例演示如何注册两个通知：

```cpp
PVOID ProcessorNotificationEntry;
PVOID MemoryNotificationEntry;
NTSTATUS Status;

Status =
  IoRegisterPlugPlayNotification(
    EventCategoryDeviceInterfaceChange,
    0,
    &GUID_DEVICE_PROCESSOR,
    DriverObject,
    AsyncProcessorCallback,
    NULL,
    &ProcessorNotificationEntry
    );

Status =
  IoRegisterPlugPlayNotification(
    EventCategoryDeviceInterfaceChange,
    0,
    &GUID_DEVICE_MEMORY,
    DriverObject,
    AsyncMemoryCallback,
    NULL,
    &MemoryNotificationEntry
    );
```

**注意**   如果设备驱动程序只需收到有关处理器的通知，则无需为内存实现回调函数或注册以获取有关内存的通知。 同样，如果只需通知设备驱动程序的内存，则无需为处理器实现回调函数或注册以获取有关处理器的通知。

 

如果设备驱动程序必须停止接收异步驱动程序通知（例如，卸载时），则它必须通过调用 [**IoUnregisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification) 函数取消注册每个回调函数。 下面的代码示例演示如何注销回调函数：

```cpp
// Unregister for asynchronous notifications
Status =
  IoUnregisterPlugPlayNotification(
    ProcessorNotificationEntry
    );

Status =
  IoUnregisterPlugPlayNotification(
    MemoryNotificationEntry
    );
```

 

