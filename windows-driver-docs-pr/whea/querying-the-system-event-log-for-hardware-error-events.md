---
title: 查询系统事件日志中的硬件错误事件
description: 查询系统事件日志中的硬件错误事件
ms.assetid: e2290a1b-6fde-4843-9c52-17279f93a887
keywords:
- WDK WHEA，查询系统事件日志的事件
- 查询系统事件日志 WDK WHEA
- 记录 WDK WHEA
- WHEA WDK，查询系统事件日志
- Windows 硬件错误体系结构 WDK，查询系统事件日志
- 事件日志 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1788b6db8a6e6af67f789f582fb5a21a7fe77322
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340697"
---
# <a name="querying-the-system-event-log-for-hardware-error-events"></a>查询系统事件日志中的硬件错误事件


记录硬件错误事件提供程序的名称如下所示：

-   **Microsoft Windows 内核 WHEA** (Windows Vista)。

-   **Microsoft Windows WHEA 记录器**（Windows Server 2008、 Windows Vista SP1 和更高版本）。

### <a name="windows-vista"></a>Windows Vista

下面的代码示例显示如何查询系统事件日志，以检索 WHEA 以前未记录任何硬件错误事件。

```cpp
// Function to query the event log for hardware error events
VOID QueryHwErrorEvents(VOID) {

  EVT_HANDLE QueryHandle;
  EVT_HANDLE EventHandle;
  ULONG Returned;

  // Obtain a query handle to the system event log
  QueryHandle =
    EvtQuery(
      NULL, 
      L"System", 
      L"*[System/Provider[@Name=\"Microsoft-Windows-Kernel-WHEA\"]]",
      EvtQueryChannelPath | EvtQueryForwardDirection
      );

  // Check result
  if (QueryHandle != NULL) {

    // Get the next hardware error event
    while (EvtNext(
             QueryHandle,
             1,
             &EventHandle,
             -1,
             0,
             &Returned
             )) {

      // Process the hardware error event
      ProcessHwErrorEvent(EventHandle);

      // Close the event handle
      EvtClose(EventHandle);
    }

    // Close the query handle
    EvtClose(QueryHandle);
  }
}
```

### <a name="windows-server-2008-windows-vista-sp1-and-later-versions"></a>Windows Server 2008、 Windows Vista SP1 和更高版本

下面的代码示例显示如何查询系统事件日志，以检索 WHEA 以前未记录任何硬件错误事件。

```cpp
// Function to query the event log for hardware error events
VOID QueryHwErrorEvents(VOID) {

  EVT_HANDLE QueryHandle;
  EVT_HANDLE EventHandle;
  ULONG Returned;

  // Obtain a query handle to the system event log
  QueryHandle =
    EvtQuery(
      NULL, 
      L"System", 
      L"*[System/Provider[@Name=\"Microsoft-Windows-WHEA-Logger\"]]",
      EvtQueryChannelPath | EvtQueryForwardDirection
      );

  // Check result
  if (QueryHandle != NULL) {

    // Get the next hardware error event
    while (EvtNext(
             QueryHandle,
             1,
             &EventHandle,
             -1,
             0,
             &Returned
             )) {

      // Process the hardware error event
      ProcessHwErrorEvent(EventHandle);

      // Close the event handle
      EvtClose(EventHandle);
    }

    // Close the query handle
    EvtClose(QueryHandle);
  }
}
```

**请注意**  的所有**Evt * Xxx*** 函数和 EVT\_*XXX*上一示例中使用的数据类型均记录在[Windows 事件日志](https://go.microsoft.com/fwlink/p/?linkid=81187)Microsoft Windows SDK 文档中的部分。

 

 

 




