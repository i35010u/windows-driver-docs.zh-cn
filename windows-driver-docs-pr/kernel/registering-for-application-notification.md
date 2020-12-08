---
title: 注册应用程序通知
description: 注册应用程序通知
keywords:
- 动态硬件分区 WDK，应用程序通知
- 硬件分区 WDK 动态，应用程序通知
- 为 WDK 动态硬件分区，应用程序通知
- 应用程序通知 WDK 动态硬件分区，注册
- 通知 WDK 动态硬件分区，应用程序
- 注册应用程序通知 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a1e017ac8471a5971c0df41ae7e94de4bfbe036
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793517"
---
# <a name="registering-for-application-notification"></a>注册应用程序通知


用户模式应用程序会调用 [RegisterDeviceNotification](/windows/win32/api/winuser/nf-winuser-registerdevicenotificationa) 函数，以便在将处理器或内存模块动态添加到硬件分区时，自行注册以获得通知。 应用程序将调用 **RegisterDeviceNotification** 函数两次，一次用于注册以获取处理器事件的通知，并在第二次注册以获取内存事件的通知。 当应用程序注册这些事件的通知时，该应用程序指定以下 Guid 之一：

<a href="" id="guid-device-processor"></a>GUID \_ 设备 \_ 处理器  
注册在将处理器动态添加到硬件分区时要通知的应用程序。

<a href="" id="guid-device-memory"></a>GUID \_ 设备 \_ 内存  
注册在将内存动态添加到硬件分区时要通知的应用程序。

这些 Guid 在头文件 Poclass 中定义。

下面的代码示例演示如何注册两个通知：

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

**注意**   如果应用程序只需收到有关处理器的通知，则无需注册内存事件通知。 同样，如果应用程序只需收到有关内存的通知，则无需注册处理器事件的通知。

 

当应用程序不再需要接收处理器或内存事件的通知时，它可以通过调用 UnregisterDeviceNotification 函数，取消注册该窗口，使其无法 \_ 为这些[UnregisterDeviceNotification](/windows/win32/api/winuser/nf-winuser-unregisterdevicenotification)事件接收 WM DEVICECHANGE 消息。 下面的代码示例演示如何取消注册应用程序通知：

```cpp
// Unregister the application window from receiving
// WM_DEVICECHANGE messages for processor events.
UnregisterDeviceNotification(ProcessorNotifyHandle);

// Unregister the application window from receiving
// WM_DEVICECHANGE messages for memory events.
UnregisterDeviceNotification(MemoryNotifyHandle);
```

有关 **RegisterDeviceNotification** 和 **UnregisterDeviceNotification** 函数的详细信息，请参阅 Microsoft Windows SDK 文档。

 

