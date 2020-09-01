---
title: 关闭与筛选器引擎建立的会话
description: 关闭与筛选器引擎建立的会话
ms.assetid: e145fb8c-fe9f-4834-8df0-f2ceb5b13b09
keywords:
- Windows 筛选平台标注驱动程序 WDK，关闭会话
- 标注驱动程序 WDK Windows 筛选平台，关闭会话
- 筛选引擎 WDK Windows 筛选平台
- 关闭筛选器引擎会话 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c8c06ead9c483768fd8a47277d4981485c3d099
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218167"
---
# <a name="closing-a-session-to-the-filter-engine"></a>关闭与筛选器引擎建立的会话


标注驱动程序执行所需的管理任务后，应关闭与筛选器引擎的会话。 标注驱动程序通过调用 [**FwpmEngineClose0**](/windows-hardware/drivers/ddi/fwpmk/nf-fwpmk-fwpmengineclose0) 函数来实现此功能。 例如：

```C++
status =
 FwpmEngineClose0(
 engineHandle  // An handle to the open session
    );
```

 

