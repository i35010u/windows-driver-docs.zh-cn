---
title: 与筛选器引擎建立会话
description: 与筛选器引擎建立会话
keywords:
- Windows 筛选平台标注驱动程序 WDK，打开会话
- 标注驱动程序 WDK Windows 筛选平台，打开会话
- 筛选引擎 WDK Windows 筛选平台
- 打开筛选器引擎会话 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 714009021fd0c6a488e8e1d48de5065f8c20363c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802281"
---
# <a name="opening-a-session-to-the-filter-engine"></a>与筛选器引擎建立会话


标注驱动程序必须与筛选器引擎建立会话，才能执行管理任务，例如向筛选器引擎添加筛选器。 标注驱动程序通过调用 [**FwpmEngineOpen0**](/windows-hardware/drivers/ddi/fwpmk/nf-fwpmk-fwpmengineopen0) 函数打开与筛选器引擎的会话。 例如：

```cpp
HANDLE engineHandle;
NTSTATUS status;

// Open a session to the filter engine
status =
 FwpmEngineOpen0(
    NULL,              // The filter engine on the local system
    RPC_C_AUTHN_WINNT, // Use the Windows authentication service
    NULL,              // Use the calling thread's credentials
    NULL,              // There are no session-specific parameters
    &engineHandle      // Pointer to a variable to receive the handle
    );
```

标注驱动程序成功打开到筛选器引擎的会话后，它可以使用返回的句柄来调用其他 Windows 筛选平台管理功能。

 

