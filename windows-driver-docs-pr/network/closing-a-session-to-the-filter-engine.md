---
title: 关闭与筛选器引擎的会话。
description: 关闭与筛选器引擎的会话。
ms.assetid: e145fb8c-fe9f-4834-8df0-f2ceb5b13b09
keywords:
- Windows 筛选平台标注驱动程序 WDK、 关闭会话
- 标注驱动程序 WDK Windows 筛选平台，关闭会话
- 筛选器引擎 WDK Windows 筛选平台
- 关闭筛选引擎会话 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ab0edc9e4e4c9225c7007f141cd25e037ab3173
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543086"
---
# <a name="closing-a-session-to-the-filter-engine"></a>关闭与筛选器引擎的会话。


标注驱动程序执行所需的管理任务后，它应关闭筛选器引擎的会话。 标注驱动程序将这是通过调用[ **FwpmEngineClose0** ](https://msdn.microsoft.com/library/windows/hardware/ff550072)函数。 例如：

```C++
status =
 FwpmEngineClose0(
 engineHandle  // An handle to the open session
    );
```

 

 





