---
title: 查询系统事件日志中的硬件错误事件
description: 查询系统事件日志中的硬件错误事件
keywords:
- 事件 WDK WHEA，查询系统事件日志
- 查询系统事件日志 WDK WHEA
- 记录 WDK WHEA
- WHEA WDK，查询系统事件日志
- Windows 硬件错误体系结构 WDK，查询系统事件日志
- 事件日志 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7be26b754dd0fefcf5ae418d3ecdf59b286619da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783671"
---
# <a name="querying-the-system-event-log-for-hardware-error-events"></a>查询系统事件日志中的硬件错误事件


记录硬件错误事件的提供程序的名称如下所示：

-   **WHEA** (windows Vista) 。

-   **WHEA** (windows Server 2008、WINDOWS Vista SP1 及更高版本) 的记录器。

### <a name="windows-vista"></a>Windows Vista

下面的代码示例演示如何查询系统事件日志，以检索先前由 WHEA 记录的任何硬件错误事件。

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

### <a name="windows-server-2008-windows-vista-sp1-and-later-versions"></a>Windows Server 2008、Windows Vista SP1 及更高版本

下面的代码示例演示如何查询系统事件日志，以检索先前由 WHEA 记录的任何硬件错误事件。

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

**注意** **Evt_Xxx_** \_ Microsoft Windows SDK 文档中的 [Windows 事件日志](/windows/win32/wes/windows-event-log)部分介绍了前面的示例中使用的所有 Evt_Xxx_ 函数和 .evt *Xxx* 数据类型。

 

 

