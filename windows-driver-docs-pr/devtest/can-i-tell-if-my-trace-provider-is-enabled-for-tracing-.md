---
title: 如果我的跟踪提供程序可用于跟踪判断
description: 如果我的跟踪提供程序可用于跟踪判断
ms.assetid: 8cc4e364-a0bc-4ef3-af3c-c08f3183b548
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c101336fe38d88594ef84a79fc61f79730fce9a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375381"
---
# <a name="can-i-tell-if-my-trace-provider-is-enabled-for-tracing"></a>能否判断是否为跟踪启用了跟踪提供程序？


是的可以使用 WPP\_级别\_已启用宏告知是否您[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序，可用于跟踪和启用的标志。 这是在跟踪提供程序额外的工作原理为软件跟踪准备特别有用。

例如，可以使用窗体的一项条件：

```
If (WPP_LEVEL_ENABLED(flag) {
            // Tracing is enabled
            Prepare to trace
            DoTraceMessage(flag...);
}
```

 

 





