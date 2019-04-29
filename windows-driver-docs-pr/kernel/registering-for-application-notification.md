---
title: 注册应用程序通知
description: 注册应用程序通知
ms.assetid: e8f76014-6068-4012-96c6-88ea2bbd9bbf
keywords:
- 动态硬件分区 WDK，应用程序通知
- 硬件分区 WDK 动态、 应用程序通知
- 分区 WDK 动态硬件，应用程序通知
- 应用程序通知 WDK 动态硬件分区、 注册
- 通知 WDK 动态硬件分区，应用程序
- 注册应用程序通知 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eccfca8f876d600dc789e4425a4665ec895b9e11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373869"
---
# <a name="registering-for-application-notification"></a>注册应用程序通知


在用户模式应用程序调用[RegisterDeviceNotification](https://go.microsoft.com/fwlink/p/?linkid=97892)函数注册自己的处理器或内存模块动态添加到硬件分区时收到通知。 应用程序调用**RegisterDeviceNotification**函数两次，一次，以注册通知的处理器事件和第二次的内存事件通知注册。 应用程序指定以下 Guid 之一时它会注册这些事件的通知：

<a href="" id="guid-device-processor"></a>GUID\_设备\_处理器  
注册该应用程序，一个处理器动态添加到硬件分区时收到通知。

<a href="" id="guid-device-memory"></a>GUID\_设备\_内存  
注册该应用程序内存动态添加到硬件分区时收到通知。

在标头文件中，Poclass.h 定义这些 Guid。

下面的代码示例演示如何注册这两个通知：

```cpp
HWND hWnd;
DEV_BROADCAST_DEVICEINTERFACE ProcessorFilter;
DEV_BROADCAST_DEVICEINTERFACE MemoryFilter;
HDEVNOTIFY ProcessorNotifyHandle;
HDEVNOTIFY MemoryNotifyHandle;

// The following example assumes that hWnd already
// contains a handle to the application window that
// is to receive the WM_DEVICECHANGE messages.

// Initialize the filter for processor event notification
ZeroMemory(
  &ProcessorFilter,
  sizeof(ProcessorFilter)
  );
ProcessorFilter.dbcc_size =
  sizeof(DEV_BROADCAST_DEVICEINTERFACE);
ProcessorFilter.dbcc_devicetype =
  DBT_DEVTYP_DEVICEINTERFACE;
ProcessorFilter.dbcc_classguid =
  GUID_DEVICE_PROCESSOR;

// Register the application window to receive
// WM_DEVICECHANGE messages for processor events.
ProcessorNotifyHandle =
  RegisterDeviceNotification(
    hWnd,
    &ProcessorFilter,
    DEVICE_NOTIFY_WINDOW_HANDLE
    );

// Initialize the filter for memory event notification
ZeroMemory(
  &MemoryFilter,
  sizeof(MemoryFilter)
  );
MemoryFilter.dbcc_size =
  sizeof(DEV_BROADCAST_DEVICEINTERFACE);
MemoryFilter.dbcc_devicetype =
  DBT_DEVTYP_DEVICEINTERFACE;
MemoryFilter.dbcc_classguid =
  GUID_DEVICE_MEMORY;

// Register the application's window to receive
// WM_DEVICECHANGE messages for memory events.
MemoryNotifyHandle =
  RegisterDeviceNotification(
    hWnd,
    &MemoryFilter,
    DEVICE_NOTIFY_WINDOW_HANDLE
    );
```

**请注意**  如果应用程序只具有要将通知处理器，它无需注册的内存事件通知。 同样，如果应用程序只具有要将通知内存，它没有注册的处理器事件通知。

 

当应用程序不再具有接收通知的处理器或内存事件时，它可以取消注册接收 WM 窗口\_通过调用这些事件的 DEVICECHANGE 消息[UnregisterDeviceNotification](https://go.microsoft.com/fwlink/p/?linkid=97893)函数。 下面的代码示例演示如何取消注册应用程序通知：

```cpp
// Unregister the application window from receiving
// WM_DEVICECHANGE messages for processor events.
UnregisterDeviceNotification(ProcessorNotifyHandle);

// Unregister the application window from receiving
// WM_DEVICECHANGE messages for memory events.
UnregisterDeviceNotification(MemoryNotifyHandle);
```

有关详细信息**RegisterDeviceNotification**并**UnregisterDeviceNotification**函数，请参阅 Microsoft Windows SDK 文档。

 

 




