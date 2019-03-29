---
title: 什么是软件跟踪的性能成本
description: 什么是软件跟踪的性能成本
ms.assetid: 4337a619-58aa-4ad2-8873-6cbf5d84d074
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b4ead4614d0640f0ecd41a0b11d4884ecc4ec3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575688"
---
# <a name="what-is-the-performance-cost-of-software-tracing"></a>软件跟踪的性价比如何？


一般情况下，软件跟踪的性能成本是非常小。 代码最小化、 有效地管理缓冲区和消息写入二进制格式。 此外，这将显著的性能降低，格式化跟踪消息会推迟到用户选择的格式和显示跟踪消息。

当你使用[WPP 软件跟踪](wpp-software-tracing.md)宏，以将软件添加到驱动程序跟踪，没有几乎没有任何性能开销，除非跟踪会话启用的提供程序。

WPP 宏量与三个条件检查中 If 语句与软件跟踪代码。 这些检查可防止除非启用的提供程序生成任何跟踪消息。 WPP 宏生成以下形式的代码：

```
If (WPP_CHECK_INIT && WPP_LEVEL_FLAGS_ENABLED) {
    Call trace_message_routine
}
```

在此生成的代码，WPP\_检查\_INIT 包含一个条件检查。 WPP\_级别\_标志\_已启用包含一个条件检查，如果您只有一个级别或标记筛选器。 否则为 WPP\_级别\_标志\_已启用包括两个条件检查。

有关详细信息，了解如何排除 WPP\_检查\_INIT 检查更好的性能，请参阅[可以优化 WPP 宏生成之前跟踪的条件检查？](can-i-optimize-the-conditional-checks-that-the-wpp-macros-produce-befo.md)。

> [!NOTE]
> 如果使用 WPP 软件跟踪之外的方法在您的驱动程序中实施软件跟踪，则可能存在某些性能成本。 效果取决于实现方法。
