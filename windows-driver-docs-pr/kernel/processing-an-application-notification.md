---
title: 处理应用程序通知
description: 处理应用程序通知
ms.assetid: 475d8e37-5d31-4989-92ce-3c4a7c09d292
keywords:
- 动态硬件分区 WDK，应用程序通知
- 硬件分区 WDK 动态、 应用程序通知
- 分区 WDK 动态硬件，应用程序通知
- 应用程序通知 WDK 动态硬件分区、 注册
- 通知 WDK 动态硬件分区，应用程序
- 注册应用程序通知 WDK 动态硬件分区
- 处理应用程序通知 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a780005ded4256076083aef8a343957bd80b72e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526134"
---
# <a name="processing-an-application-notification"></a>处理应用程序通知


在用户模式应用程序如何处理 WM\_DEVICECHANGE 消息取决于是否在应用程序基于纯粹是针对 Win32 API 或是否基于 Microsoft 基础类 (MFC) 库。

### <a name="win32-applications"></a>Win32 应用程序

基于 Win32 的应用程序处理的消息发送到应用程序的窗口的实现*窗口过程*。 有关窗口过程的详细信息，请参阅[窗口过程](https://go.microsoft.com/fwlink/p/?linkid=96748)Microsoft Windows SDK 文档中的主题。

下面的代码示例演示如何处理 WM\_DEVICECHANGE 基于 Win32 的应用程序中的消息：

```cpp
// Prototype for the function that handles the
// processing of WM_DEVICECHANGE messages.
LRESULT
OnDeviceChange(
  WPARAM wParam,
  LPARAM lParam
  ); 

// The application&#39;s message processing function
// for the window that receives the WM_DEVICECHANGE
// messages.
LRESULT CALLBACK
WindowProc(
  HWND hWnd,
  UINT uMsg,
  WPARAM wParam,
  LPARAM lParam
  )
{
  switch (uMsg)
  {
      .
      .  // Cases for other messages
      .
    // Device change message
    case WM_DEVICECHANGE:
      OnDeviceChange(wParam, lParam);
      break;
      .
      .  // Cases for other messages
      .
    // Catchall for all messages that are
    // not handled by the application.
    default:
      return DefWindowProc(
               hWnd,
               uMsg,
               wParam,
               lParam
               );
  }

  return 0;
}

// The function that handles the processing
// of WM_DEVICECHANGE messages.
LRESULT
OnDeviceChange(
  WPARAM wParam,
  LPARAM lParam
  )
{
  PDEV_BROADCAST_HDR devHdr;
  PDEV_BROADCAST_DEVICEINTERFACE devInterface;
  HANDLE ProcessHandle;
  DWORD_PTR ProcessAffinityMask;
  DWORD_PTR SystemAffinityMask;
  DWORD_PTR ChangedAffinityMask;
  MEMORYSTATUSEX MemoryStatus;

  // Check whether the message is a device arrival message
  if (wParam == DBT_DEVICEARRIVAL)
  {
    // Get a pointer to the structure header
    devHdr = (PDEV_BROADCAST_HDR)lParam;

    // Check whether the message is about a device interface
    if (devHdr->dbch_devicetype == DBT_DEVTYP_DEVICEINTERFACE)
    {
      // Get a pointer to the device interface structure
      devInterface = (PDEV_BROADCAST_INTERFACE)devHdr;

      // Check whether this is a message about a processor
      if (IsEqualGUID(
            devInterface->dbcc_classguid,
            GUID_DEVICE_PROCESSOR
            ))
      {
        // Get a handle to the current process
        ProcessHandle =
          GetCurrentProcess();

        // Get the current process and system affinity masks
        GetProcessAffinityMask(
          ProcessHandle,
          &ProcessAffinityMask,
          &SystemAffinityMask
          );

        // Get a mask of any change to the set of processors
        ChangedAffinityMask =
          ProcessAffinityMask ^ SystemAffinityMask;

        // Perform any per processor memory allocation
        // for any new processors
        ...

        // Set the process affinity mask to use all the
        // active processors in the hardware partition.
        SetProcessAffinityMask(
          ProcessHandle,
          SystemAffinityMask
          );

        // Adjust the number of threads in any thread
        // pools as needed for optimal performance.
        ...
      }

      // Check whether this is a message about memory
      else if (IsEqualGUID(
                 devInterface->dbcc_classguid,
                 GUID_DEVICE_MEMORY
                 ))
      {
        // Get the current memory status
        GlobalMemoryStatusEx(&MemoryStatus);

        // Note: MemoryStatus.ullTotalPhys contains
        // the amount of physical memory in the
        // hardware partition.

        // Adjust the memory buffer allocations
        // as needed for optimal performance.
        ...
      }
    }
  }

  return 0;
}
```

### <a name="mfc-applications"></a>MFC 应用程序

MFC 框架处理发送到基于 MFC 的应用程序窗口的消息。 基于 MFC 的应用程序必须实现[OnDeviceChange](https://go.microsoft.com/fwlink/p/?linkid=97894)接收 WM 的应用程序的窗口类的成员函数\_DEVICECHANGE 消息。

下面的代码示例演示如何实现**OnDeviceChange**基于 MFC 的应用程序中的成员函数：

```cpp
afx_msg BOOL
CAppWnd::OnDeviceChange(
  UINT nEventType,
  DWORD_PTR dwData
  )
{
  PDEV_BROADCAST_HDR devHdr;
  PDEV_BROADCAST_DEVICEINTERFACE devInterface;
  HANDLE ProcessHandle;
  DWORD_PTR ProcessAffinityMask;
  DWORD_PTR SystemAffinityMask;
  DWORD_PTR ChangedAffinityMask;
  MEMORYSTATUSEX MemoryStatus;

  if (nEventType == DBT_DEVICEARRIVAL)
  {
    devHdr = (PDEV_BROADCAST_HDR)dwData;

    if (devHdr->dbch_devicetype == DBT_DEVTYP_DEVICEINTERFACE)
    {
      devInterface = (PDEV_BROADCAST_INTERFACE)devHdr;

      if (IsEqualGUID(
            devInterface->dbcc_classguid,
            GUID_DEVICE_PROCESSOR
            ))
      {
        // Get a handle to the current process
        ProcessHandle =
          GetCurrentProcess();

        // Get the current process and system affinity masks
        GetProcessAffinityMask(
          ProcessHandle,
          &ProcessAffinityMask,
          &SystemAffinityMask
          );

        // Get a mask of any change to the set of processors
        ChangedAffinityMask =
          ProcessAffinityMask ^ SystemAffinityMask;

        // Perform any per processor memory allocation
        // for the new processors
        ...

        // Set the process affinity mask to use all the
        // active processors in the hardware partition.
        SetProcessAffinityMask(
          ProcessHandle,
          SystemAffinityMask
          );

        // Adjust the number of threads in any thread
        // pools as needed for optimal performance.
        ...
      }
      else if (IsEqualGUID(
                 devInterface->dbcc_classguid,
                 GUID_DEVICE_MEMORY
                 ))
      {
        // Get the current memory status
        GlobalMemoryStatusEx(&MemoryStatus);

        // Note: MemoryStatus.ullTotalPhys contains
        // the amount of physical memory in the
        // hardware partition.

        // Adjust the memory buffer allocations
        // as needed for optimal performance.
        ...
      }
    }
  }

  return TRUE;
}
```

 

 




