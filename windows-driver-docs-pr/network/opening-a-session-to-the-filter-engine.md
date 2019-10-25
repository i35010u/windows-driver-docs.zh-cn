---
title: 与筛选器引擎建立会话
description: 与筛选器引擎建立会话
ms.assetid: 23db0e2d-7f27-4323-801c-346e14f0f83e
keywords:
- Windows 筛选平台标注驱动程序 WDK，打开会话
- 标注驱动程序 WDK Windows 筛选平台，打开会话
- 筛选引擎 WDK Windows 筛选平台
- 打开筛选器引擎会话 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c54fd6bf706ee5208d50e08a9462514fec0dcda
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843762"
---
# <a name="opening-a-session-to-the-filter-engine"></a>与筛选器引擎建立会话


标注驱动程序必须与筛选器引擎建立会话，才能执行管理任务，例如向筛选器引擎添加筛选器。 标注驱动程序通过调用[**FwpmEngineOpen0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpmk/nf-fwpmk-fwpmengineopen0)函数打开与筛选器引擎的会话。 例如：

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

 

 





