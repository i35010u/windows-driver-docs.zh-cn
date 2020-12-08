---
title: 注册获取硬件错误事件通知
description: 注册获取硬件错误事件通知
keywords:
- 事件 WDK WHEA，注册通知
- 注册硬件事件通知
- 通知 WDK WHEA
- WHEA WDK，注册事件通知
- Windows 硬件错误体系结构 WDK，注册事件通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 096b98da9882811c47b91992cd77fd40385d72ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832041"
---
# <a name="registering-for-notification-of-hardware-error-events"></a>注册获取硬件错误事件通知


若要注册以获得有关新硬件错误事件的通知，应用程序将创建对 WHEA 提供程序引发的所有事件的订阅。 WHEA 提供程序的名称是 **WHEA**。

WHEA 提供程序引发硬件错误事件的通道如下所示：

-   **System** 信道 (Windows Vista) 。

-   **WHEA** 信道 (windows Server 2008 和 WINDOWS Vista SP1) 。

-   Windows 7 及更高版本)  (**WHEA/Errors** 通道。

### <a name="windows-vista"></a>Windows Vista

下面的代码示例演示如何注册此版本 Windows 的新硬件错误事件的通知。

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

### <a name="windows-server-2008-windows-vista-sp1-and-later-versions"></a>Windows Server 2008、Windows Vista SP1 及更高版本

下面的代码示例演示如何为这些版本的 Windows 注册新硬件错误事件的通知。

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

**注意** 在 **Evt*Xxx** \_ Microsoft Windows SDK 文档的 [Windows 事件日志](/windows/win32/wes/windows-event-log)部分中介绍了前面的示例中使用的所有 .evt * Xxx * 函数和 .evt *Xxx* 数据类型。

 

 

