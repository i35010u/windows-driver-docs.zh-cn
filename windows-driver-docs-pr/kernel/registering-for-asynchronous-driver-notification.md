---
title: 注册为异步的驱动程序通知
description: 注册为异步的驱动程序通知
ms.assetid: e1f97a65-7c82-4d7b-97ec-0293fc69fd8c
keywords:
- 驱动程序通知 WDK 动态硬件分区、 注册
- 异步通知 WDK 动态硬件分区
- 通知--WDK 各种动态的硬件，分区、 注册
- 异步驱动程序通知 WDK 动态硬件分区、 注册
- 注册的驱动程序通知 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d6c2de67b4a1094cc4779e72e6ec5d16270fb1d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544266"
---
# <a name="registering-for-asynchronous-driver-notification"></a>注册为异步的驱动程序通知


若要使用异步驱动程序通知，设备驱动程序实现到硬件分区动态添加处理器或内存模块时，操作系统将调用的回调函数。 下面的代码示例显示了此类回调函数的原型：

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

设备驱动程序通过调用注册异步通知[ **IoRegisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549526)函数，为每个设备驱动程序的回调函数，指定一个指针，一次以下 Guid 之一*EventCategoryData*参数：

<a href="" id="guid-device-processor"></a>GUID\_设备\_处理器  
注册一个处理器动态添加到硬件分区时收到通知。

<a href="" id="guid-device-memory"></a>GUID\_设备\_内存  
注册内存动态添加到硬件分区时收到通知。

在标头文件中，Poclass.h 定义这些 Guid。

下面的代码示例演示如何注册这两个通知：

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

**请注意**  如果设备驱动程序仅包含要将通知处理器，它无需实现回调函数的内存或注册内存有关的通知。 同样，如果设备驱动程序仅包含要将通知内存，它没有实现处理器的回调函数或注册有关处理器的通知。

 

当设备驱动程序必须停止接收异步驱动程序通知，例如当正在卸载它，它必须通过调用来取消注册每个回调函数[ **IoUnregisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff550398)函数。 下面的代码示例演示如何取消注册回调函数：

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

 

 




