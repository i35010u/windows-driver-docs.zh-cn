---
title: 注册获取硬件错误事件通知
description: 注册获取硬件错误事件通知
ms.assetid: 86816fc7-fa69-4ecf-9d50-822b0fa6992d
keywords:
- 事件 WDK WHEA，注册通知
- 注册硬件事件通知
- 通知 WDK WHEA
- WHEA WDK，注册的事件通知
- Windows 硬件错误体系结构 WDK，注册的事件通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab7fc5a19fdfade3d64daaae0bc842057080e641
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340677"
---
# <a name="registering-for-notification-of-hardware-error-events"></a>注册获取硬件错误事件通知


若要注册以获得有关新的硬件错误事件的通知，应用程序创建由 WHEA 提供程序引发的所有事件的订阅。 WHEA 提供程序的名称是**Microsoft Windows 内核 WHEA**。

WHEA 提供程序将硬件错误事件引发的通道是按如下所示：

-   **系统**通道 (Windows Vista)。

-   **Microsoft Windows 内核 WHEA**通道 （Windows Server 2008 和 Windows Vista SP1）。

-   **Microsoft-Windows-内核的 WHEA/错误**通道 （Windows 7 和更高版本）。

### <a name="windows-vista"></a>Windows Vista

下面的代码示例演示如何注册此版本的 Windows 的新硬件错误事件的通知。

```cpp
// Prototype for the notification callback function
DWORD WINAPI HwErrorEventCallback(
  EVT_SUBSCRIBE_NOTIFY_ACTION Action,
  PVOID Context,
  EVT_HANDLE EventHandle
  );

// Function to create a subscription to all hardware error
// events that are raised by the WHEA provider.
EVT_HANDLE SubscribeHwErrorEvents(VOID)
{
  EVT_HANDLE SubHandle;

  // Create a subscription to all events that are sent to
  // the System channel by the WHEA provider.
  SubHandle =
    EvtSubscribe(
      NULL,
      NULL,
      L"System", 
      L"*[System/Provider[@Name=\"Microsoft-Windows-Kernel-WHEA\"]]",
      NULL,
      NULL,
      HwErrorEventCallback,
      EvtSubscribeToFutureEvents
      );

   // Return the subscription handle
   return SubHandle;
}

// Notification callback function
DWORD WINAPI HwErrorEventCallback(
  EVT_SUBSCRIBE_NOTIFY_ACTION Action,
  PVOID Context,
  EVT_HANDLE EventHandle
  )
{
  // Check the action
  if (Action == EvtSubscribeActionDeliver) {

    // Process the hardware error event
    ProcessHwErrorEvent(EventHandle);
  }

  // Return success status
  return ERROR_SUCCESS;
}

// Function to terminate the subscription
VOID UnsubscribeHwErrorEvents(EVT_HANDLE SubHandle)
{
  // Close the subscription handle
  EvtClose(SubHandle);
}
```

### <a name="windows-server-2008-windows-vista-sp1-and-later-versions"></a>Windows Server 2008、 Windows Vista SP1 和更高版本

下面的代码示例演示如何注册新的这些版本的 Windows 的硬件错误事件的通知。

```cpp
// Prototype for the notification callback function
DWORD WINAPI HwErrorEventCallback(
  EVT_SUBSCRIBE_NOTIFY_ACTION Action,
  PVOID Context,
  EVT_HANDLE EventHandle
  );

// Function to create a subscription to all hardware error
// events that are raised by the WHEA provider.
EVT_HANDLE SubscribeHwErrorEvents(VOID)
{
  EVT_HANDLE SubHandle;

  // Create a subscription to all events that are sent
  // to the WHEA channel.
#if (WINVER <= _WIN32_WINNT_LONGHORN)
  SubHandle =
    EvtSubscribe(
      NULL,
      NULL,
      L"Microsoft-Windows-Kernel-WHEA", 
      L"*",
      NULL,
      NULL,
      HwErrorEventCallback,
      EvtSubscribeToFutureEvents
      );
#else
  SubHandle =
    EvtSubscribe(
      NULL,
      NULL,
      L" Microsoft-Windows-Kernel-WHEA/Errors", 
      L"*",
      NULL,
      NULL,
      HwErrorEventCallback,
      EvtSubscribeToFutureEvents
      );
#endif

   // Return the subscription handle
   return SubHandle;
}

// Notification callback function
DWORD WINAPI HwErrorEventCallback(
  EVT_SUBSCRIBE_NOTIFY_ACTION Action,
  PVOID Context,
  EVT_HANDLE EventHandle
  )
{
  // Check the action
  if (Action == EvtSubscribeActionDeliver) {

    // Process the hardware error event
    ProcessHwErrorEvent(EventHandle);
  }

  // Return success status
  return ERROR_SUCCESS;
}

// Function to terminate the subscription
VOID UnsubscribeHwErrorEvents(EVT_HANDLE SubHandle)
{
  // Close the subscription handle
  EvtClose(SubHandle);
}
```

**请注意**  的所有**Evt * Xxx*** 函数和 EVT\_*XXX*上一示例中使用的数据类型均记录在[Windows 事件日志](https://go.microsoft.com/fwlink/p/?linkid=81187)Microsoft Windows SDK 文档中的部分。

 

 

 




