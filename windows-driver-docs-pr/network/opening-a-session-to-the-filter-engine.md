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
ms.openlocfilehash: 46a3b49bf2b5ad3c0fca3dc5ff90ddfc001a7d15
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366557"
---
# <a name="opening-a-session-to-the-filter-engine"></a>与筛选器引擎建立会话


标注驱动程序必须打开与筛选器引擎来执行管理任务，例如将筛选器添加到筛选器引擎的会话。 标注驱动程序打开一个到会话筛选器引擎通过调用[ **FwpmEngineOpen0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpmk/nf-fwpmk-fwpmengineopen0)函数。 例如：

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

 

 





