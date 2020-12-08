---
title: 能否判断跟踪提供程序是否已启用跟踪
description: 能否判断跟踪提供程序是否已启用跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 293f62e60c3aad7127e6d149b878a5abae2fabcf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786393"
---
# <a name="can-i-tell-if-my-trace-provider-is-enabled-for-tracing"></a>能否判断是否为跟踪启用了跟踪提供程序？


是的，你可以使用启用了 WPP \_ 级别的 \_ 宏来指示 [跟踪提供程序](trace-provider.md)（如内核模式驱动程序或用户模式应用程序）是否已启用跟踪以及启用了哪些标志。 如果跟踪提供程序执行了额外的工作来准备软件跟踪，这会特别有用。

例如，你可以使用以下形式的条件：

```
If (WPP_LEVEL_ENABLED(flag) {
            // Tracing is enabled
            Prepare to trace
            DoTraceMessage(flag...);
}
```

 

 





