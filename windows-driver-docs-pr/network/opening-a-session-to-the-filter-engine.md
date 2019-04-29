---
title: 与筛选器引擎建立会话
description: 与筛选器引擎建立会话
ms.assetid: 23db0e2d-7f27-4323-801c-346e14f0f83e
keywords:
- Windows 筛选平台标注驱动程序 WDK，打开会话
- 标注驱动程序 WDK Windows 筛选平台，打开会话
- 筛选器引擎 WDK Windows 筛选平台
- 打开筛选器引擎会话 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455f6b34ad5e1bc6551de23406673649cf5136bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384227"
---
# <a name="opening-a-session-to-the-filter-engine"></a>与筛选器引擎建立会话


标注驱动程序必须打开与筛选器引擎来执行管理任务，例如将筛选器添加到筛选器引擎的会话。 标注驱动程序打开一个到会话筛选器引擎通过调用[ **FwpmEngineOpen0** ](https://msdn.microsoft.com/library/windows/hardware/ff550075)函数。 例如：

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

标注驱动程序已成功打开与筛选器引擎的会话后，它可以使用返回的句柄来调用其他 Windows 筛选平台管理功能。

 

 





