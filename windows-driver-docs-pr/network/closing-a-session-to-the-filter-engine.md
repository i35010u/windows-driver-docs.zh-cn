---
title: 关闭与筛选器引擎建立的会话
description: 关闭与筛选器引擎建立的会话
keywords:
- Windows 筛选平台标注驱动程序 WDK，关闭会话
- 标注驱动程序 WDK Windows 筛选平台，关闭会话
- 筛选引擎 WDK Windows 筛选平台
- 关闭筛选器引擎会话 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54fb316347a0d0c93aed4a22440b05080901a516
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782289"
---
# <a name="closing-a-session-to-the-filter-engine"></a>关闭与筛选器引擎建立的会话


标注驱动程序执行所需的管理任务后，应关闭与筛选器引擎的会话。 标注驱动程序通过调用 [**FwpmEngineClose0**](/windows-hardware/drivers/ddi/fwpmk/nf-fwpmk-fwpmengineclose0) 函数来实现此功能。 例如：

```C++
status =
 FwpmEngineClose0(
 engineHandle  // An handle to the open session
    );
```

 

